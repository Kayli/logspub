## kubernetes k8s

## basics

- kubectl (cube cuddle) is cli for k8s
- minikube provides simple local k8s cluster
- helm is a k8s package manager
- object definitions
  - define desired state
    - controllers watch object definitions to achieve that state
  - often defined in yaml file format, but there are json and cli alternatives


## key entities

- specification
  - yaml or json file of the predefined format
  - defines configuration for k8s entities
  - can be executed by
    > kubectl apply -f <myspec.yaml>

- control plane (ex master node)
  - has 4 processes
    - api server: gateway to the cluster
    - scheduler: decides on which node to host individual pods
    - controller manager: monitors/recovers cluster state
    - etcd: stores cluster state/configuration data (not application data!)

- node (ex worker node)
  - is a vm or a physical computer that serves as a worker machine in a kubernetes cluster
  - has processes
    - kubelet: starts the pod with a container inside
    - container runtime, e.g. docker
    - kube proxy: intelligently manages connections between pods
  - hosts multiple pods
  
- pod
  - smallest deployable units of computing that you can create and manage in k8s
  - can have one or more containers inside
  - provides a context with shared storage and network resources
  - has specification for how to run the containers
  - pods are running on a private, isolated network inside k8 cluster
  - don't have a stable ip/dns name, as it is randomized after recreation

- service
  - takes care of service discovery, allowing to expose
    - fixed ip
    - dns, in case if addon installed
      - cluster-aware DNS server, such as CoreDNS, watches the Kubernetes API for new Services and creates a 
        set of DNS records for each one. If DNS has been enabled throughout your cluster then all Pods should
        automatically be able to resolve services by their DNS name [^4]
  - pods can have labels and service can load-balance between pods using selector mechanism
  - when a pod is run on a node, the kubelet adds a set of environment variables for each active service

- ingress
  - set of rules to pass to a controller that is listening for them. 
  - you can deploy a bunch of ingress rules, but nothing will happen unless you have a controller that can process them

- ingress controller
  - a pod that is configured to interpret ingress rules
    - one of the most popular ingress controllers supported by kubernetes is nginx
  - in terms of amazon, alb can be used as an ingress controller

- deployment
  - defines/configures pods and replica sets via deployment controller
    - replica set defines how many pod instances we need across cluster
  - abstraction on top of pods
  - may be described as yaml with desired state [^1]
    > kubectl apply -f <myconfig.yaml>
  - or created using direct cli command
    > kubectl create deployment <name> --image=<image-name>

- stateful set
  - like a deployment, a statefulset manages pods that are based on an identical container spec
  - make it easier to match existing volumes to the new Pods that replace any that have failed
  - provide you with [^3]
    - a predictable name
      - you want to start your pods telling them where to find each other so they can form a cluster, elect a leader, etc. 
        but you need to know their names in advance to do that. Normal pod names are random so you can't know them in advance
    - stable address/DNS name
      - if a normal pod restarts on another host it'll get a new name and a new IP address
    - persistent link between pod and its persistent volume
      - if you redeploy your group of 3 database hosts you want the same individual (by DNS name and IP address) 
        to get the same persistent volume so the master is still the master and still has the same data

- persistent volume
  - local or remote storage for stateful apps
  - is not bound to any namespace
- persistent volume claim
  - generalized request for some part of a storage

- cloud cluster: what you run in production, consists of min 2 master and 3 worker nodes

- config map: used to store non-confidential data in key-value pairs
- secret: object that contains a small amount of sensitive data such as a password, a token, or a key


## databases

- etcd
  - distrubuted key-value store 
  - uses raft consensus algorithm to elect master node for writes
  - can i use it for my apps somehow as well? should i deploy another etcd cluster?

- kubegres
  - postgresql cluster operator
  - manages fail-over 
  - has a data backup option allowing to dump PostgreSql data regularly in a given volume

- patterns
  - sidecar
    - there are 2 containers in a single pod
      - main app
      - sidecar
    - goal: augment functionality of main app in some way


## typical scenarios

- configure environment
  - install minikube
  - install helm
    > sudo snap install helm --classic
  - run proxy to be able to access deployed pods and services using ugly request string
    > kubectl proxy
    > curl -I http://127.0.0.1:8001/api/v1/namespaces/default/services/SERVICE-NAME:PORT/proxy/
  - alternatively, run tunnel to expose cluster services to host machine via external ips
    > minikube tunnel
  - alternatively, map port from pod to host machine
    > kubectl -n default port-forward $POD_NAME 8443:8443
    
- deploy application from container image, exposing port 80 on a pod
  > kubectl create deployment hellonginx --image=nginxdemos/hello --port=80

- expose deployment with its pod as a service
  > kubectl expose deployment hellonginx --type=LoadBalancer --name=hellonginx-service
  
- get information
  > kubectl get deployments
  > kubectl get pods
  > kubectl describe pods
  > kubectl get services

- scale deployment
  > kubectl scale deployment hellonginx --replicas=3
  > kubectl get pods -o wide
  
- delete existing deployment
  > kubectl delete deployment hellonginx

- start shell session in the pod's container
  > kubectl get pods
  > kubectl exec -ti <pod-name> -- sh


## helm charts

- chart 
  - is a collection of files that describe a related set of Kubernetes resources. 
  - a single chart might be used to deploy something simple, like a memcached pod, or something complex, 
    like a full web app stack with HTTP servers, databases, caches, and so on
  - runs template engine for kubernetes manifest files, which enables more flexible k8 deployments

- mustache syntax
  - enables more flexible (but less readable) templates
  - in a spirit of xslt

- values files
  - is used to parametrize generic chart with specifics that we need in each particular case
  - multiple values files for different environments: values-dev.yaml, values-qa.yaml

- tpl files
  - allows to put reusable pieces of transformation logic, 

- advantages
  - easily prototype an application installation
  - non-final values are separated from actual objects (parametrization)
  - many applications can be deployed through a single chart instance
  - in a template you can check nested values at every level (conditionals)

- popular charts
  - dashboard https://github.com/kubernetes/dashboard
    - create a new user, otherwise it wont work!!
    - to authenticate with token, decode and view it with the following command
      > kubectl get secrets
      > kubectl get secret <secret-name> -o jsonpath={.data.token} | base64 -d
    - create kubeconfig file
      > kubectl config view > kubeconfig
    - add 'token' field for the user with decoded token as a value [^2]
  - etcd https://artifacthub.io/packages/helm/bitnami/etcd

- registry
  - https://artifacthub.io/
  - https://github.com/cdwv/awesome-helm


## operators

- operator
  - custom form of controllers
  - it takes human operational knowledge and encodes it into software that is more easily packaged 
    and shared with consumers
  - watches over your k8 environment and uses its current state to make decisions in milliseconds

- operator framework https://operatorframework.io
  - set of developer tools and k8s components, that aid in operator development and central 
    management on a multi-tenant cluster

- capability levels https://operatorframework.io/operator-capabilities/
- registry https://operatorhub.io


## secrets

- helm secrets
  - enable safe storage of encrypted secrets in git
    - private key used to decrypt secrets is stored only on a cluster
  - supports aws kms
  - but strongly coupled to Helm

- bitnami sealed secrets project

- hashicorp vault
  - sealed by default
  - uses shamir's secret sharing algorithm
    - you need to distribute several (5) keys among team members, so each team member has one key
    - min 3 keys are required to unseal the vault
    - you need to manually unseal every node in a cluster


## security, shift-left

- datree
  - statically checks resource definition yamls for schema compliance and good-practice policies
  - cli tool with some web ui for managing policies

- rbac mechanism implement access control rules 
  - its based on defining crud rules for a user about whats allowed and not

- gatekeeper open policy agent (opa)
  - allows to define rules for allowed node types to be provisioned, resource limits, etc.
  - validation happens at 'run-time', so resources may end up being partially provisioned
  - uses 'rego' dsl to define logic for policies


## gitops or infrastructure as code (iac)

- gitlab via
  - gitops workflow [^6]
    - uses gitlab agent installed on k8 cluster, automatic polling approach
  - ci/cd workflow [^6]
    - uses k8 api to manage cluster, proactive push approach
  - terraform integration
    - so that manifest files can be written as a terraform script and applied automatically

- portainer [^5]
  - allows to monitor changes to manifest files stored in git and automatically apply them

- argo

- some additional info
  - https://medium.com/style-theory-engineering/infrastructure-as-code-kubernetes-a2f050389f26


## tools to consider

- k3s [^7]
  - a lightweight k8 orchestrator
  - 40mb ram footprint, can run on raspberry pi
  - simple to setup
  - lacks: high availability, zero downtime cluster upgrades
- k9s: simple terminal-based status monitoring tool
- rancher desktop (cli+gui)
  - kim is a wrapper for docker commands
- velero https://github.com/vmware-tanzu/velero
  - gives you tools to back up and restore your kubernetes cluster resources and persistent volumes
- chaoskube https://github.com/linki/chaoskube
  - chaosmonkey implementation
- envoy https://github.com/slamdev/helm-charts/tree/master/charts/envoy
  - service mesh implementation using sidecar pattern for tracebility and a bunch of other features
- tilt https://tilt.dev
  - gives you smart rebuilds and live updates without having to go through ci/cd pipeline
  - used to speedup coding with dev clusters
- zabbix monitoring https://github.com/zabbix
- shift-left, policy management
  - datree: cli tool to validate yaml for schema compliance and good-practice policies
  - gatekeeper open policy agent (opa)
  - kyverno


## tutorials

- aws eks with terraform https://www.youtube.com/watch?v=Qy2A_yJH5-o
- introduction to helm https://www.youtube.com/watch?v=5_J7RWLLVeQ
- gitlab, k8s, helm integration example https://www.youtube.com/watch?v=8Ao5WcMJJ2c
- gitlab: automating k8s deployments https://www.youtube.com/watch?v=wEDRfAz6_Uw


## references

[^1]: https://kubernetes.io/docs/tutorials/stateless-application/expose-external-ip-address/
[^2]: https://stackoverflow.com/questions/70287656/kubernetes-dashboard-internal-error-500-not-enough-data-to-create-auth-info
[^3]: https://stackoverflow.com/questions/41732819/why-statefulsets-cant-a-stateless-pod-use-persistent-volumes
[^4]: https://kubernetes.io/docs/concepts/services-networking/service/#dns
[^5]: https://youtu.be/FC8pABzxZVU?t=1660
[^6]: https://docs.gitlab.com/ee/user/clusters/agent/
[^7]: https://youtu.be/ePyFJ7Hd57Q?t=967
