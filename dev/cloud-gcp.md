# notes google cloud platform

## basics

- lists over 100 products under the google cloud brand
- mostly used
  - compute
  - storage
  - ci/cd


## compute

- compute engine: customizable vms

- kubernetes engine (gke)
  - free tier: provides $74.40 in monthly credits per billing account

- app engine
  - does not require app to be containerized

- cloud run
  - based on knative
    - is a platform-agnostic solution for running serverless deployments
  - no vendor lock-in
    - app components should be containerized
  - zero-configuration fast autoscaling
    - efficient: uses no resources if there are no requests
  - supports blue-green and canary deployments
  - automatic redundancy
  - stateless, ephemeral containers
  - execution time limit: 15 minutes

- athos
  - google's proprietary container and vms orchestrator
  - simplifies edge deployments
  - integrates on-prem with cloud components
  - integrates service mesh

- cloud functions
  - functions as a service (faas) to run event-driven code written in Node.js, Java, Python, or Go.


## storage [3]

- cloud storage
  - is an 'object storage' which is good for
    - blobs, object data
    - unstructured data like media, docs, logs, backups, application binaries, vm images
  - 'buckets' are the basic containers that hold your data
  - main characteristics: available, durable, secure    
  
  - location types
    - regional: data stored redundantly in a single region
      - best for high-performance analytics where data needs to be collocated with compute
    - multi-region
      - stored redundantly across the continent
      - not visible which regions your data is in
    - dual-region
      - best for datalakes for streaming, etl and ml projects
  
  - storage classes
    - standard (snappiest)
    - nearline
    - coldline
    - archive (cheapest, but there are retrieval fees and min duration constraint)
  - automatically transition data to lower-cost storage based on user-defined lifecycle rules
  
  - offers some s3 compatability, devil is in details [1]
  - auto versioning

- cloud storage transfer tools
  - help to upload data from computer to the cloud
  - gsutil: rsync-like incremental copies, multithreaded, also helps managing gcs buckets

- other transfer services
  - storage transfer service, transfer appliance, bigquery data transfer service
  - helps with migration and moving things around

- filestore
  - data is organized into files and folders
  - fully managed network attached storage (nas)

- persistent disk
  - is a block data storage
  - stores evenly-sized blocks of binary data
  - is not aware of the filesystem
  - offers higher performance and lower latency
  - other block storage gcp services: local ssd
  - can be mounted to cloud run gen2 instances [2]


## databases

- cloud sql
  - relational database service
  - fully managed, proprietary
  - offers compatability with mysql, postgresql, and sql server apis
    - database migration service (dms): offers simplified data migration procedures


## ci/cd

- cloud build (automate builds and other tasks, aka jenkins)

- artifact registry https://cloud.google.com/artifact-registry
  - considered 'the next generation of container registry'
  - supports
    - container images
    - os packages for Debian and RPM
    - language packages for popular languages like Python, Java, and Node

- google cloud deployment manager
  - is an infrastructure deployment service
  - automates the creation and management of google cloud resources
    - using template and configuration files
  - something like terraform and pulumi, but gcp native, locked-in


## other gcp services

- sandbox environments
  - cloud code (remote dev environments)


## useful commands

- set default parameters
  > gcloud config set compute/zone us-west1-a

- get list of containers
  > gcloud container images list --repository="gcr.io/deeplearning-platform-release"

- manage GCP compute instances within free tier defaults
  - create new instance
    > gcloud compute instances create vm01 --image-project debian-cloud --image-family debian-11 --machine-type=e2-micro
  - create new instance based on a docker image (only images hosted on gcr are supported)
    > gcloud compute instances create-with-container <instance-name> --container-image <image-name> --machine-type=e2-micro
  
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
  - if you still can't connect, try populating ssh config on your local machine automatically
    > gcloud compute config-ssh 

- manage firewall
  - create new rule to allow all inbound traffic for all instances
    > gcloud compute firewall-rules create allow-all --direction=INGRESS --action=ALLOW --priority=500
        --project=rock-module-342604 --network=default --rules=all
  - disable/enable rule
    > gcloud compute firewall-rules update allow-all --disabled --project=rock-module-342604
    > gcloud compute firewall-rules update allow-all --no-disabled --project=rock-module-342604


## costs

- free tier: one e2-micro instance
- machine image $0.05 gb/month (typical debian image is about 10GB)


## useful information

- container registry https://cloud.google.com/container-registry
  - is deprecated on may 2023, superseeded by artifact registry


## references

[1]: https://vamsiramakrishnan.medium.com/a-study-on-using-google-cloud-storage-with-the-s3-compatibility-api-324d31b8dfeb
[2]: https://stackoverflow.com/questions/64228967/how-to-mount-persistent-storage-to-google-cloud-run
[3]: https://cloud.google.com/blog/topics/developers-practitioners/introducing-visualizing-google-cloud-101-illustrated-references-cloud-engineers-and-architects
