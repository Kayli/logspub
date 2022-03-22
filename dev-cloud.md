# notes on topics related to cloud computing


## commonly used terms

- infrastructure as a service (iaas)
  - virtualization and management of servers, operating systems, networks, and storage
  
- platform as a service (paas)
  - ci/cd, dbms, bi services on top of iaas

- software as a service (saas)
  - cloud-first apps built on top of iaas and paas  


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

- docker
- kubernetes k8s
  - key entities
    - node
      - controller
      - worker
    - pod
    - service
    - replica set
      - defines how many pod instances we need across cluster
    - deployment
      - yaml with desired state
      - defines/configures pods and replica sets via deployment controller
      - abstraction on top of pods
    - volume
      - local or remote storage for stateful apps
    - stateful set
      - provides replication services for volumes

- integration projects
  - is a project that tries to integrate a bunch of smaller projects while making money selling consultancy services
  - recipe
    - just generate a bunch of <your favorite language> wrappers around some more popular community-driven components
    - give them some funny names to create a customer-engaging story
    - say its sponsored or originated by nasa or something
      - bend the truth as much as you can, just to sell shit

  - projects caught my attention recently
    - openstack
      - written in: python
      - supported by the "open infrastructure foundation" (openinfra foundation)
        - wikipedia says that original founders are Rackspace Hosting and NASA
      - website feels like a marketing blob vaguely explaining how to configure services in a cloud
      - most likely goals are 
        - to provide overview (possibly twisted) of a cloud services landscape
        - generate leads
      - can be viewed as an ideological adapter/lens through which cloud prescribed to be percieved
      - root repository https://github.com/openstack/openstack
      - red flags
        - why when browsing through a list of their components i rarely recognize anything as familiar
          - are they living in some parallel universe or somehting?
          
    - openshift
      - developer: redhat
      - written in: go, angular.js
      - an on-premises platform as a service
        - built around docker containers orchestrated and managed by kubernetes 
          on a foundation of red hat enterprise linux
- monitoring
  - cloudkeeper https://github.com/someengineering/cloudkeeper

## azure services

- azure data services 
  - sql database/sql managed instance
  - analysis services [^2]
    - tabular data model: in-memory table, highly compressed
  - synapse
    - for big data, sharding
  - cosmos db (many different apis to access same data)
  - hdinsight (kafka, hbase, hadoop mapreduce)
  - databricks
  - azure data factory - etl, transforming and moving data around
  - azure ml - machine learning training and stuff


## google cloud platform

- some stuff to be aware of
  - sudo command on ubuntu instance is not working when connecting via external ssh client
      - use `su` instead
    - you can change root password via web ssh client by running `sudo passwd` command
    - to connect with external ssh client
      - generate ssh key on your client machine
        > ssh-keygen -t rsa -f ~/.ssh/<key> -C <username> -b 2048
      - copy public key (file contents) to remote machine's ~/.ssh/authorized_keys file
      - connect to gcp machine using following command:
        - ssh -i /Users/illiak/.ssh/<key> <username>@<public_ip_address>
      - alternatively, you can add public key from cloud shell terminal
        - gcloud compute os-login ssh-keys add --key-file=<your_pubkey_file>
  - start instance from cloud shell terminal
    > gcloud compute instances start instance-1 --zone=us-west4-b


## references

[^1]: https://en.wikipedia.org/wiki/OpenShift
[^2]: https://www.youtube.com/watch?v=R7k4qJ120dY
