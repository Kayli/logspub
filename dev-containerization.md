# notes about containerization and related topics

## basics

- open container initiative (oci)
  - standards around container technology
  - compliant: docker, containerd, cri-o


## docker

- definition
  - a set of tools that use OS-level virtualization to deliver software in packages called containers
  - containers are isolated from one another and bundle their own software, libraries and configuration files
    - they can communicate with each other through well-defined channels

- state is not preserved after restarting container by default
  - unless you're using a docker volume

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

- risks of executing more than one process per container [^5]
  - the process that forked and went background is not monitored and may stop without you knowing it


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
[^5]: https://stackoverflow.com/questions/37458287/how-to-run-a-cron-job-inside-a-docker-container
