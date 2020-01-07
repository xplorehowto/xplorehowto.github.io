---
title: Technology - Docker
keywords: software, technology, container, docker
tags: [technology, container, docker]
sidebar: coding_sidebar
permalink: /coding_docker
folder: coding
---

## Installing Docker on Linux Debian

- Installation using Docker provided script; the script will detect hardware
  platform automatically; see below for manual installation steps.
```bash
sudo apt-get update
sudo apt-get dist-upgrade -y
curl -sSL get.docker.com | sh
```
  Note: if the download fails, as shown below, retry again;
```
[...]
+ sudo -E sh -c echo "deb [arch=armhf] https://download.docker.com/linux/raspbian stretch stable" > /etc/apt/sources.list.d/docker.list
+ sudo -E sh -c apt-get update -qq >/dev/null
W: Failed to fetch http://raspbian.raspberrypi.org/raspbian/dists/stretch/InRelease  Temporary failure resolving 'raspbian.raspberrypi.org'
W: Failed to fetch https://download.docker.com/linux/raspbian/dists/stretch/InRelease  Could not resolve host: download.docker.com
W: Failed to fetch http://archive.raspberrypi.org/debian/dists/stretch/InRelease  Temporary failure resolving 'archive.raspberrypi.org'
W: Some index files failed to download. They have been ignored, or old ones used instead.
+ [ -n  ]
+ sudo -E sh -c apt-get install -y -qq --no-install-recommends docker-ce >/dev/null
E: Unable to locate package docker-ce
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
```bash
sudo usermod pi -aG docker
newgrp docker
sudo reboot now
```

### *Manual installation* of Docker on Linux Debian

Manual installation steps provide details that will be useful during 
troubleshooting;

**References:**  
- [https://docs.docker.com/install/linux/docker-ce/ubuntu/](https://docs.docker.com/install/linux/docker-ce/ubuntu/)


**Steps for first time on a new host machine:**    
Set up the Docker repository before installing Docker CE. 
Installation and update of docker image will be pulled from the repository.

- First, update the apt package index:
```bash
sudo apt-get update
```

- Install packages to allow apt to use a repository over HTTPS:
```bash
sudo apt-get install --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

- Add Docker’s official GPG key:
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

- Verify that the key with the fingerprint,  
  `9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88`, 
  by matching the last 8 characters of the fingerprint.
```bash
sudo apt-key fingerprint 0EBFCD88
    
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```

- Set up the stable repository for x86_64/amd64. 
  To add the nightly or test repository, add the word `nightly` or `test` 
  (or both) after the word `stable` in the commands below. 
  See references for other architectures.
```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
  **Note:** the `lsb_release -cs` sub-command returns the name of 
  Ubuntu distribution, such as xenial. 


**INSTALL Docker CE**  

- Update the apt package index.
```bash
sudo apt-get update
```

- Install the latest version of Docker CE and containerd:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
  - To install a specific version of Docker CE, first list the available 
    versions in the repo, then select and install:
    ```
    apt-cache madison docker-ce
    
    docker-ce | 5:18.09.1~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
    docker-ce | 5:18.09.0~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
    docker-ce | 18.06.1~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
    docker-ce | 18.06.0~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
    ...
    ```
  -  Install a specific version using the version string from the second column,
     for example, 5:18.09.1~3-0~ubuntu-xenial.
    ```
    sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
    ```

- VERIFY that Docker CE is installed correctly by running the hello-world image
```
sudo docker run hello-world
```


## Enter running container

```
docker container run -it --rm --name sample alpine /bin/sh
```

## Remove all stop process
```
docker rm $(docker ps -a -q)
```


## Transfer image between host without using docker image repository

Ideally, the docker image is shared using the docker repository. However, if
docker repository is not readily available, use the following `docker save` and
`docker load` to transfer the image between host. To rebuild using the provided
scripts is also an option, but some build could take a long time.  

```bash
# export to the intended folder; first change directory to the folder
#docker save -o <path for generated tar file> <image name>
cd ~
docker save -o ./arm32v7-alpine_3-9-3.tar arm32v7-alpine:3.9.3

# transfer file to destination host, usinf SCP for example

# import
#docker load -i <path to image tar file>
cd ~
docker load -i ./arm32v7-alpine_3-9-3.tar
```
