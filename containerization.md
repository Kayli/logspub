# notes about containerization and related topics

## docker

- definition
  - a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers
  - containers are isolated from one another and bundle their own software, libraries and configuration files
    - they can communicate with each other through well-defined channels


- installation
  - on arch, run following commands from terminal
    ```bash
	  pamac install docker
	  
	  sudo systemctl start docker.service
	  sudo systemctl enable docker.service

	  sudo groupadd docker						# this allows unprivileged users to get root access. 
	  sudo usermod -aG docker $USER

	  docker run hello-world					# run test container to make sure everything works
	```

- running x-server application within a container
  - https://github.com/mviereck/x11docker

- running container overriding default CMD [^1]
  - $ docker run -it --entrypoint=/bin/bash <image>


### dockerfile basic commands

- RUN
  - executes commands inside of your Docker image during build time
  - get written into your Docker image as a new layer
- CMD
  - default command to run when your container starts
  

## references

[^1]: https://serverfault.com/questions/594281/how-can-i-override-cmd-when-running-a-docker-image
