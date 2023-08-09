# notes about openshift orchestration platform

## basics

- developed, supported, sponsored by red hat and world community
  - ibm aquired redhat in 2019

- provides higher-level abstractions on top of k8s to simplify distributed applications
  - also makes learning curve for k8s more gradual

- 'oc' command
  - performs the same role in OpenShift as kubctl in kubernetes

- official name of the product: 'Red Hat OpenShift Container Platform'


## oc commands

- describe: similar to inspect in docker


## examples

- runs oc describe to read the information from etcd about a pod named simplehttp:
  > oc describe pod/simplehttp
