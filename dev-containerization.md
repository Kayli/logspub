# notes about containerization and related topics

## docker

- definition
  - a set of tools that use OS-level virtualization to deliver software in packages called containers
  - containers are isolated from one another and bundle their own software, libraries and configuration files
    - they can communicate with each other through well-defined channels

- installation
  - on arch, run following commands from terminal
	  > pamac install docker
	  > sudo systemctl start docker
	  > sudo systemctl enable docker
	  > sudo groupadd docker						# this allows unprivileged users to get root access
	  > sudo usermod -aG docker $USER
	  > docker run hello-world					# run test container to make sure everything works

- running x-server application within a container using x11docker [^2]
- running container overriding default CMD [^1]
  > docker run -it --entrypoint=/bin/bash <image>

- copy file from inside of the running docker container
  > docker ps -alq # get last container id
  > docker cp <containerId>:/file/path/within/container /host/path/target

- dockerfile basic commands
  - FROM <image> [as <stage>]
  - COPY [--from=<stage>] <src> <dst>
  - RUN
    - executes commands inside of your Docker image during build time
    - get written into your Docker image as a new layer
  - CMD
    - default command to run when your container starts

- optimization
  - combine RUN commands into one using && to avoid creating extra layers [^3]


## kubernetes k8s

- to run locally 
  - minikube (cli only)
  - rancher desktop (cli+gui)
    - kim is a wrapper for docker commands

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

- databases
  - etcd
    - distrubuted key-value store 
    - uses raft consensus algorithm to elect master node for writes

  - kubegres [^5]
    - postgresql cluster operator
    - manages fail-over 
    - has a data backup option allowing to dump PostgreSql data regularly


     in a given volume

- patterns
  - sidecar
    - there are 2 containers in a single pod
      - main app
      - sidecar
    - goal: augment functionality of main app in some way

- dapr (distributed application runtime) [^4]
  - unified wrapper for pubsub, rpc, configuration, instrumentation
  - can use redis for pubsub
    - can be run in 'append only file' mode with fsync at every query to provide stong guarantees


## other useful tools

- portainer
  - centralized service delivery platform for containerized apps (docker, k8s)
  - deploy and see the state of individual containers, restart them and debug them when necessary
    - all without needing to use the command line


## references

[^1]: https://serverfault.com/questions/594281/how-can-i-override-cmd-when-running-a-docker-image
[^2]: https://github.com/mviereck/x11docker
[^3]: https://docs.docker.com/develop/develop-images/multistage-build/
[^5]: https://www.kubegres.io/doc/getting-started.html
[^4]: https://www.youtube.com/watch?v=-4sHUvfk2Eg

