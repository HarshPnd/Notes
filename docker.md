# Docker Command quick reference

 A concise guide to docker commands and their outputs.


> # [How to install Docker](/how%20to%20install%20docker-ce%20in%20rhel8.md)



>##  `docker ps`
- list running containers.
---



>##  `docker ps -a`
- list all (running + stopped) containers.
---



>##  `docker run -it --name os1 centos:7`
- starts a container using centos version 7 image (if the image is not already downloaded then it will automatically be downloaded from docker hub) here `-t` stands for terminal (because we want to use the terminal of the container) and `-i` stand for iterative/interactive (because we want the terminal to be iterative and we want to interact with the terminal) `--name` is used to provide the name (os1) to the container if the name is not given then a random name is generated.
---



>##  `docker rm os1`
- Removes a stopped container whose name is os1.
---


>##  `docker rm -f os1`
- Removes a running container whose name is os1.
---


>##  `docker ps -a -q`
- list the container id of all running + stopped containers.
---

>##  `docker rm -f $(docker ps -aq)`
- Removes all the containers (running & stopped).
---



>##  `curl -sSL https://get.docker.com | sh`
- used to install docker.
---


>##  `docker version`
- lists the info about installed docker version.
---



>##  `docker images`
- lists all the downloaded docker images.
---



>##  `docker pull centos:7`
- download centos version 7 image from docker hub.
---


>##  `docker info`
- displays the information of the installed version of docker.
---


>##  `exit`
- Used to shut-down and exit the running container.
---


>##  `Ctrl+p+q`
- used toexit a running container but the container keeps running in background.
---


>##  `docker attach os1`
- Used to attach to the container with the name os1 running in background.
---


>##  `docker rmi centos:7`
- Remove centos:7 image.
---



>##  `docker help`
- list all docker commands.
---


>##  `docker stop os1`
- used to stop container `os1` from outside the container.
---

>##  `docker commit os1 myimage:v1`
- Commit and create a new image `myimage` withe the version `v1` of a container `os1`.
---
