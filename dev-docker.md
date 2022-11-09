# notes about containerization and related topics

## basics

- definition
  - a set of tools that use OS-level virtualization to deliver software in packages called containers
  - containers are isolated from one another and bundle their own software, libraries and configuration files
    - they can communicate with each other through well-defined channels

- open container initiative (oci)
  - standards around container technology
  - compliant: docker, containerd, cri-o

- state is not preserved after restarting container by default
  - unless you're using a docker volume


## installation

- on arch, run following commands from terminal
  > pamac install docker
  > sudo systemctl start docker
  > sudo systemctl enable docker
  > sudo groupadd docker						# this allows unprivileged users to get root access
  > sudo usermod -aG docker $USER
  > docker run hello-world					# run test container to make sure everything works

- fish completions (official)
  > wget https://raw.githubusercontent.com/docker/cli/master/contrib/completion/fish/docker.fish -O ~/.config/fish/completions/docker.fish


## running container from image

- simplest use, just run container from an image in a background
  > docker run <image>

- run a process within a container from specified image, make sure its interactive and attach current terminal to it
  > docker run --interactive --tty <image> <process>
  > docker run -it <image> <process>                  # shorter version of the command above

- assign name and start tty
  > docker run -it --name <name> <image>

- run ubuntu with bash
  > docker run -it ubuntu bash

- running container overriding default [^1] entrypoint 
  > docker run -it --entrypoint=/bin/bash <image>

- run container from image, removing all existing containers created from that image
  > docker run --rm -it <image> <process>

- running x-server application within a container using x11docker [^2]

- copy file from inside of the running docker container
  > docker ps -alq # get last container id
  > docker cp <containerId>:/file/path/within/container /host/path/target

- risks of executing more than one process per container [^5]
  - the process that forked and went background is not monitored and may stop without you knowing it
 
 - start container in a detached mode saving its id
  > CID=$(docker run -d <image> <process>)


## run process in already running container

- docker exec [OPTIONS] <container> [command] [arg...]


## persistence

- named volume
  > docker volume create <volume_name> 
  > docker run -v <volume_name>:/etc/<volume_name> <image>

- view mounts
  > docker inspect -f '{{ .Mounts }}' <container_id>


## build an image

- dockerfile basic commands
  - FROM <image> [as <stage>]
  - COPY [--from=<stage>] <src> <dst>
  - RUN
    - executes commands inside of your Docker image during build time
    - get written into your Docker image as a new layer
  - CMD
    - default command to run when your container starts

- .dockerignore files are an easy way to selectively copy only image relevant files

- optimization
  - combine RUN commands into one using && to avoid creating extra layers [^3]

- view sbom (software bill of materials)
  > docker sbom <image>

- check with snyk for vulnerabilities
  > docker scan <image> 

- 'entrypoint' and 'cmd'
  - used to specify a default command on container start

- docker build
  > docker build .                          # builds image from Dockerfile in a current folder
  > docker build --file <dockerfile>        # builds image from dockerfile
  > docker build --rm --file <dockerfile>   # removes intermediate containers after successful build
  > docker build --progress=plain .         # builds and displays all output, while default behavior is to show build messages only briefly

- custom build arguments
  - allows you to parametrize your dockerfile
  - declare args
    - FROM alpine:latest
    - ARG EXAMPLE_VAR
    - ARG DEMO_VAR='some default val'
  - pass args
    > docker build -t example-image:latest --build-arg EXAMPLE_VAR=value1 --build-arg DEMO_VAR=value2 .

- dependencies
  - when there are several dockerfiles that form a hierarchy, there is no single command to build whole dependency chain
    - to address this, multistage dockerfiles should be used


## useful commands

- run bash process inside already running container 
  > docker exec -it <container> bash


## docker compose

- defines docker-compose.yml file with configuration
- helps with 
  - running multiple containers together
  - storing configuration settings
    - such as volume mounts for the container
    - port mappings
    - environment variables
- to start containers
  > docker-compose up


## alternatives

- podman
  - runs docker containers in userspace, rootless installation
  - does not support compose files out of the box, but podman-compose project addresses that
  - supports k8s specification yaml files
    > podman play kube myspec.yml
  - doesn't work on my macos

- colima
  - allows running docker containers in userspace, enables rootless docker
  - to get started, run
    > brew install colima
    > colima start


## other useful tools

- portainer
  - centralized service delivery platform for containerized apps (docker, k8s)
  - deploy and see the state of individual containers, restart them and debug them when necessary
    - all without needing to use the command line


## problems

- can't locate docker images in wsl
  - it works somehow differently whem using docker desktop


## references

[^1]: https://serverfault.com/questions/594281/how-can-i-override-cmd-when-running-a-docker-image
[^2]: https://github.com/mviereck/x11docker
[^3]: https://docs.docker.com/develop/develop-images/multistage-build/
[^5]: https://www.kubegres.io/doc/getting-started.html
[^4]: https://www.youtube.com/watch?v=-4sHUvfk2Eg
[^5]: https://stackoverflow.com/questions/37458287/how-to-run-a-cron-job-inside-a-docker-container
