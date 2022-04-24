## kubernetes k8s

- pods that are running inside k8 are running on a private, isolated network

- to run locally 
  - minikube (cli only)
  - rancher desktop (cli+gui)
    - kim is a wrapper for docker commands

- key entities
  - control plane (ex master node)
    - has 4 processes
      - api server: gateway to the cluster
      - scheduler: decides on which node to host individual pods
      - controller manager: monitors/recovers cluster state
      - etcd: stores cluster state/configuration data (not application data!)
  - node
    - is a vm or a physical computer that serves as a worker machine in a kubernetes cluster
    - has processes
      - kubelet: starts the pod with a container inside
      - container runtime, e.g. docker
      - kube proxy: intelligently manages connections between pods
    - hosts multiple pods
  - pod
  - service
    - takes care of service discovery, allowing to expose fixed ip 
    - see selector and load-balancer mechanisms
    - when a pod is run on a node, the kubelet adds a set of environment variables for each active service
  - ingress controller
    - component and api which allows you to expose your service as a dns endpoint
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
  - cubectl
    - cli to interact with the cluster
  - cluster types
    - cloud cluster: what you run in production, consists of min 2 master and 3 

- databases
  - etcd
    - distrubuted key-value store 
    - uses raft consensus algorithm to elect master node for writes

  - kubegres [^5]
    - postgresql cluster operator
    - manages fail-over 
    - has a data backup option allowing to dump PostgreSql data regularly in a given volume

- patterns
  - sidecar
    - there are 2 containers in a single pod
      - main app
      - sidecar
    - goal: augment functionality of main app in some way
