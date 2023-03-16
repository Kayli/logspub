# azure cloud services

## basics

- pricing tiers are associated with individual resources, not subscriptions

- resource provisioning automation
  - arm templates: are native way to declaratively provision resources from code
  - terraform: supports azure via azurerm provider


## portal

- spa for managing azure cloud resources

- user interface elements [^3]

  - page header: top line of controls
    - portal menu: where all services are listed
      - nested inside page header when collapsed, overlays on the left side when expanded

  - breadcrumb: use the breadcrumb links to move back a level in your workflow

  - resource menu (left pane)
    - commands that are contextual to your current focus
  
  - working pane (central pane)
    - details about the resource that is currently in focus
    - command bar. These controls are contextual to your current focus.

  - all resources pane (sometimes shown on the left side)
    - is undocumented, see [^3]
    - shows up when you select 'all resources' azure services on home screen


## event hubs

- terminology mapped to kafka
  - event hubs namespace  > broker
  - event hub             > topic
  - event publisher       > producer
  - event consumer        > consumer
  - consumer group
    - is a view (state, position, or offset) of an entire event hub
    - useful in publish-subscribe pattern scenario
    - but there are some complications to be aware of
      - https://stackoverflow.com/questions/54388546/what-is-consumer-group-in-azure-event-hub

- local setup
  - does not have an emulator that can be installed locally
  - you'll need to create an Event Hubs instance in Azure and use that for development and testing purposes
  - or you can use kafka instance locally
    - but make sure your code is using kafka client apis

- pricing and tiers (basic, standard, premium, dedicated) [^1]
  - number of namespaces per subscription: 1k for all plans [^2]
  - partitions per event hub: 32, 32, 100, 1024
  - event hubs per namespace:	10, 10, 100, 1k
  - throughput per unit: 1 MB/s or 1000 events per second
  - consumer groups per event hub: 1, 20, 100, 1000


## azure functions

- functions app
  - application hosting multiple azure functions
  - lightweight ASP.NET Core application running on top of Azure WebJobs SDK (old deployment model, deprecated)

- functions instance host
  - compute instance hosting single functions app
  - a unit of scale: all functions within a function app 
      - share resource within an instance
      - scale at the same time
  - each instance host: 1.5 GB of memory and 1 CPU

- triggers
  - event hubs
    - competing consumers pattern
      - consumers parallelism is limited by number of partitions of the event hub
        - e.g. max number of parallelism is the max number of event hubs instance partitions
      - function holds a lease on certain partitions, depending on how many of them are provisioned
        - for a single consumer it holds a lease
      - uses polling, which is nonsense. very bad design decision on ms side.

- scaling methods
  - running multiple functions in-parallel
  - adding more instances of the azure functions host
    - scale controller monitors the rate of events and determines whether to scale out or scale in
      - may use queue length and the age of the oldest queue message

- useful resources
  - https://learn.microsoft.com/en-us/azure/azure-functions/functions-concurrency
  - https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale
  - https://learn.microsoft.com/en-us/azure/azure-functions/event-driven-scaling


## gateways / load balancers [^4]

- app gateway
  - distributes traffic within a single region across multiple availability zones (datacenters)
  - features
    - url redirection/routing
    - url rewrite
    - request modification
    - tls termination/offload
      - can upload certificate or take from a vault
    - session affinity
    - scale/autoscale across multiple availability zones (v2)
    - waf v2 (web application firewall)
      - set waf policy with owasp automatic checks/protection
      - costs twice as much as standard v2
    - multisite (routing based on domain name)
  
  - request processing pipeline
    - frontend ip addresses: public/private
    - waf
    - listeners
      - traffic mapped to one of the registered listeners
      - matching performed based on its properties: ip, port, protocol, hostname
    - rules
      - allow more flexible routing
      - associated with only 1 listener
      - uses rules to map traffic from listeners to a set of backends
    - rewrite rules
      - header, url, cookie, querystring, etc.
      - many to many relationship with rules
    - backends

- front door (global)
  - distributes traffic across multiple regions


## useful commands

- change default subscription
  > az account set --subscription "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

- list all resources accessible for active subscription
  > az resource list

- create principal account
  - rbac roles often used: Contributor, Reader
  > az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/8a434fbd-3bfa-4121-bf21-6ce0c07c0cf4" --name="Terraform2"

- export all resources using principal account
  > aztfexport resource-group <rg-name>
  - uses oauth to authenticate by reading following vars: AZURE_CLIENT_ID, AZURE_CLIENT_SECRET, AZURE_TENANT_ID, AZURE_SUBSCRIPTION_ID
  - does not support 'az login' authentication
  - above command needs service principal account to be created and env vars set before running aztfexport, e.g.


## impressions

- back browser button is often not working appropriately in a portal

- pricing tiers are not dev friendly (very expensive)
  - you will be charged arm and leg even on your dev environments for provisioning additional resources generating minimal amounts of traffic
  - eventhub namespaces charged hourly based on throuput units specified at the namespace level
    - so if you created an eventhub namespace and it just sits there without getting any traffic - you're still paying for it
  - app gateway v2 standard: 180 usd/month for provisioning  [^5]
  
- not all resources are made equal
  - event hub instances are not displayed in the list of resources when queried via 'az resource list' command

- aztfexport tool doesn't work well with 'basic' pricing tier
  - hides errors in in interactive mode




## references

[^1]: https://learn.microsoft.com/en-us/azure/event-hubs/compare-tiers
[^2]: https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-quotas
[^3]: https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-overview
[^4]: https://www.youtube.com/watch?v=B3O6bXu-NbM
[^5]: https://azure.microsoft.com/en-ca/pricing/details/application-gateway/
[^6]: https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-faq