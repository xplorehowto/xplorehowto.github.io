---
title: Software Coding - Docker
keywords: software, development, coding, docker
tags: [software_development, coding]
sidebar: coding_sidebar
permalink: /coding_docker
folder: coding
---

## Docker

### Installing Docker on Linux Debian

- Installation

```
sudo apt-get update -y
sudo apt-get dist-upgrade -y
curl -sSL get.docker.com | sh
```

- Post installation
  Docker daemon binds to a Unix socket which is by default owned by root; 
  daemon always runs as root user. Other users access it using `sudo`.
  To allow users to run the docker commands without `sudo`, create a Unix group
  called `docker` and add users to it; when the Docker daemon starts, it creates 
  a Unix socket accessible by members of the `docker` group.  
  **Warning:** the docker group grants privileges equivalent to the root user. 
  For details on how this impacts security in your system, see 
  [Docker Daemon Attack Surface](https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface).

```
sudo usermod pi -aG docker
newgrp docker
sudo reboot
```

### Enter running container

```
docker container run -it --rm --name sample alpine /bin/sh
```

