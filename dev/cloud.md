# notes on topics related to cloud computing


## commonly used terms

- hyperscalers
  - large cloud service providers
  - can provide services such as computing and storage at enterprise scale

- infrastructure as a service (iaas)
  - virtualization and management of servers, operating systems, networks, and storage

- platform as a service (paas)
  - ci/cd, dbms, bi services on top of iaas

- software as a service (saas)
  - cloud-first apps built on top of iaas and paas

- function as a service (faas)
  - serverless hosting for app code

- service-level agreement (sla)
  - commitment between a service provider and a client
  - particular aspects of the service – quality, availability, responsibilities – are agreed
    between the service provider and the service user

- virtual private cloud (vpc) 
  - on-demand configurable pool of shared resources allocated within a public cloud environment, 
    providing a certain level of isolation between the different organizations using the resources

- region
  - geographical location where a cloud provider hosts their data centers
  - consists of multiple availability zones
  - can have different capabilities and pricing structures

- availability zone
  - physically separated data centers within the region, providing additional redundancy and fault tolerance

- provisioning automation frameworks
  - cloud-agnostic: terraform, pulumi
  - aws: cloud development kit
  - crossplane: provisioning through k8s


## closed-source cloud solutions

- amazon web services (aws)
- microsoft azure  
- google cloud platform (gcp)
- alibaba cloud
- digitalocean

- data platforms
  - snowflake
    - datalake, data warehouse
    - runs on Amazon S3 since 2014,[2] on Microsoft Azure since 2018[7] and on the Google Cloud Platform since 2019
  - databricks
    - runs spark and related services/integrations
    - has jupiter-like ide


## foss cloud solutions

- openstack
  - developer: Rackspace Hosting and NASA (original founders according to wikipedia)
  - written in: python
  - supported by the "open infrastructure foundation" (openinfra foundation)
  - root repository https://github.com/openstack/openstack

- openshift
  - developer: redhat
  - written in: go, angular.js
  - most popular as on-premises platform as a service solution
  - built around docker containers orchestrated and managed by kubernetes on a foundation of red hat enterprise linux

  - distributions
    - origin: opensource application container platform
    - online: public application development hosting service
    - dedicated: managed private cluster on aws/gcp 
    - enterprise: on-premise private paas

- monitoring
  - cloudkeeper https://github.com/someengineering/cloudkeeper


## azure

- see dev-cloud-azure.md


## aws

- see dev-cloud-aws.md


## vendor neutral

- https://github.com/dapr
- https://github.com/serverless/serverless


## how they make extra money

- azdo feeds are preserved for extra 30 days without ability to reclaim space for this period
  - when trying to delete feed, the following message gets displayed:
    "Once deleted, the feed will enter a disabled state for 30 days, after which it will be permanently deleted. In this state, packages cannot be installed, published, or manipulated and storage will not be reclaimed. You may restore the feed to its original state, or permanently delete it in the feed settings to clean up storage. This feed name may not be reused until permanently deleted."

- azdo pipelines may not stop jobs right away when parent stage gets cancelled
  - but it will wait until job finishes or errors out
  - this may be no longer true as I saw it sometimes stops the job before it finishes
    - anyways, it seems that behavior is undefined or maybe there are no guarantees that it finishes right away

- there is no way to create personal authentication (pat) token for a service account in azdo
  - so if you're using gitlab, you'll have to use pat assigned to one of your employees
  - this will introduce risks and may force ppl to adopt closed-source github and azure pipelines instead of staying foss


## serverless

- definition
  - cloud computing execution model 
  - in which the cloud provider allocates machine resources on demand, taking care of the servers on behalf of their customers

- usually contrasted with more traditional styles, such as microservices or monoliths

- devs are not concerned with
  - compute capacity planning, configuration management, maintenance, fault tolerance
  - scaling of containers, VMs, or physical servers

- implementations
  - knative
    - is a platform-agnostic solution for running serverless deployments
    - coarse features
      - functions
      - serving
      - eventing


## terminology

- rds: relational database service



## references

[1]: https://en.wikipedia.org/wiki/OpenShift
[2]: https://www.youtube.com/watch?v=R7k4qJ120dY
