# notes google cloud platform

## serivces

- lists over 100 products under the google cloud brand

- compute
  - compute engine: customizable vms
  - kubernetes engine (gke)
  - cloud run
    - based on Knative (serverless containers in kubernetes environments)
    - support for GCP, AWS and VMware management

  - athos
    - google's proprietary container and vms orchestrator
    - simplifies edge deployments
    - integrates on-prem with cloud components
    - integrates service mesh

  - cloud functions
    - functions as a service to run event-driven code written in Node.js, Java, Python, or Go.

- ci/cd
  - cloud build (automate builds and other tasks, aka jenkins)
  - container registry https://cloud.google.com/container-registry
  - artifact registry https://cloud.google.com/artifact-registry
    - considered 'the next generation of container registry'
    - supports
      - container images
      - os packages for Debian and RPM
      - language packages for popular languages like Python, Java, and Node
  
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
    > gcloud compute firewall-rules create allow-all --direction=INGRESS --action=ALLOW --priority=500 \
        --project=rock-module-342604 --network=default --rules=all
  - disable/enable rule
    > gcloud compute firewall-rules update allow-all --disabled --project=rock-module-342604
    > gcloud compute firewall-rules update allow-all --no-disabled --project=rock-module-342604

- costs
  - free tier: one e2-micro instance
  - machine image $0.05 gb/month (typical debian image is about 10GB)
