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

- openstack
  - written in: python
  - supported by the "open infrastructure foundation" (openinfra foundation)
    - wikipedia says that original founders are Rackspace Hosting and NASA
  - website feels like a marketing blob vaguely explaining how to configure services in a cloud
  - root repository https://github.com/openstack/openstack

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

- manage GCP compute instances within free tier defaults
  > gcloud compute instances create vm01 \
      --image-project debian-cloud --image-family debian-11 --zone=us-west1-a --machine-type=e2-micro
  > gcloud compute instances list
  > gcloud compute instances start <name>
  > gcloud compute ssh <name>
  > gcloud compute instances delete <name>

- google cloud doesn't provide an easy solution to backup/restore vm instances
  - you can only make a snapshot of disks attached to instances

- to connect with external ssh client
  - generate ssh key on your client machine
    > ssh-keygen -t ed25519 -C "<comment>"
  - copy public key and save as a file in a cloud shell terminal
  - add public key from cloud shell terminal
    - gcloud compute os-login ssh-keys add --key-file=<your_pubkey_file>
  - connect to gcp machine using one of the following commands
    > gcloud compute ssh <name>
    > ssh <username>@<public_ip_address>

- manage firewall
  - create new rule to allow all inbound traffic for all instances
    > gcloud compute firewall-rules create allow-all --direction=INGRESS --action=ALLOW --priority=500 \
        --project=rock-module-342604 --network=default --rules=all
  - disable/enable rule
    > gcloud compute firewall-rules update allow-all --disabled --project=rock-module-342604
    > gcloud compute firewall-rules update allow-all --no-disabled --project=rock-module-342604

- costs
  - free tier: one e2-micro instance
  - machine image $0.05 gb/month (typical debian image is about 10GB)


## aws

- compute
  - ec2: virtual machines
  - ecs: elastic container store (docker)
    - aws container orchestration platform
    - operates with clusters and tasks
  - fargate
    - run docker containers without managing any servers for container orchestration
  - lambda
    - time limit of 15 minutes per function
    - runs on ephemeral containers behind the scenes


## vendor neutral

- https://github.com/dapr
- https://github.com/serverless/serverless


## references

[^1]: https://en.wikipedia.org/wiki/OpenShift
[^2]: https://www.youtube.com/watch?v=R7k4qJ120dY
