---
layout: note
title: "Docker CLI Cheat Sheet"
date: 2022-12-30T12:00:00+00:00
tags: ["Docker","CLI","CheatSheet"]
author: "brkzr"
description: Docker CLI Cheat Sheet
---


Commonly used docker commands:

### General Commands
---
```bash
docker --help                  # first always ask help from docker --help !!!
docker system prune            # prune all system (use it carefully !)
docker version                 # docker version (-v)
docker stats                   # stats of running container
docker top <containerID>       # show process of container
docker logs <containerID>      # show logs of container
docker port <containerID>      # show mapped port of container
```

### Images & Docker Hub
---

```bash
docker search <imageName>      # search an image in Docker Hub.
docker pull <imageName>        # pull an image from Docker Hub
docker images                  # list images
docker rmi <imageName>         # delete an image
docker image prune             # remove all unused images
docker build -t <imageName> .  # build image from dockerfile. use (-no-cache) to avoid cached image

```

### Containers 
---
```bash
docker run <imageName>                  # start new container from image
docker run -d <imageName>               # run container in the background (detach)
docker run <imageName> ls -lrt /lib     # change entrypoint (--enrtypoint) 
docker run -p 8080:80 ngnix             # map a port, (host:container)
docker run -n <containerName> <imageName>   # assing a name to container (--name)
docker run -e PASSWORD=password <imageName> # assing environment value to container ()
docker run -v ~/:/usr/share <imageName>     # map local directory to container (host:container)
# docker run -it  -v ~/:/usr/share -e PASSWORD=password ubuntu /bin/bash    

docker exec -it <containerID> bash      # bash inside a running container

docker pause|unpause <containerID>      # pause / unpause (SIGSTOP signal)
docker start|stop <containerID>         # start / stop (SIGTERM or SIGKILL signal)
docker kill <containerID>               # default SIGKILL signal (--signal=SIGHUP)

docker ps -a                            # list all containers       
docker ps -aq                           # list all container id's
docker ps | tail -1 | awk '{print $1}'  # list all container id's

docker rm <containerID>                 # remove specific container (-f force)
docker rm $(docker ps -aq)              # remove all containers
docker rm `docker ps -aq`               # remove all containers
```

### Docker-Compose
> similar to docker commands 
---
```bash
docker-compose up | down        # up / down 
docker-compose unpause | pause  
docker-compose start | stop

docker-compose up -d            # run in background (detach) 

docker-compose logs
docker-compose ps
```