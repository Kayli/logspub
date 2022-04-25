## kubernetes k8s

## basics

- pods that are running inside k8 are running on a private, isolated network
- kubectl is cli for k8s
- minikube provides simple local k8 cluster
- helm is a k8 package manager


## key entities

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
  - defines/configures pods and replica sets via deployment controller
  - abstraction on top of pods
  - may be described as yaml with desired state [^1]
    > kubectl apply -f <myconfig.yaml>
  - or created using direct cli command
    > kubectl create deployment <name> --image=<image-name>

- volume
  - local or remote storage for stateful apps
- stateful set
  - provides replication services for volumes

- cloud cluster: what you run in productkubectl config view > kubeconfigion, consists of min 2 master and 3 worker nodes 


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
  - start this in a separate terminal to make external-ip available on host
    > minikube tunnel
  
- delete existing deployment
  > kubectl delete deployment hellonginx

- start shell session in the pod's container
  > kubectl get pods
  > kubectl exec -ti <pod-name> -- sh

- install dashboard https://github.com/kubernetes/dashboard
  - to authenticate with token, decode and view it with the following command
    > kubectl get secrets
    > kubectl get secret <secret-name> -o jsonpath={.data.token} | base64 -d
  - create kubeconfig file
    > kubectl config view > kubeconfig
  - add 'token' field for the user with decoded token as a value [^2]


## tools to consider

- rancher desktop (cli+gui)
  - kim is a wrapper for docker commands


## references

[^1]: https://kubernetes.io/docs/tutorials/stateless-application/expose-external-ip-address/
[^2]: https://stackoverflow.com/questions/70287656/kubernetes-dashboard-internal-error-500-not-enough-data-to-create-auth-info
