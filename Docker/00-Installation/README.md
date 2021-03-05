# Installation

First we must know which distribution and OS we will run Docker over to import those specific repositories.

In this section we will explain how to install it for Ubuntu, but if you have other Linux distro or OS, go to the [official documentation](https://docs.docker.com/engine/install/).

## Remove old versions

```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

## Update repositories, install dependencies and add repositories

```
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
## Install Docker

```
 $ sudo apt-get update
 $ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
## Test if it's correctly installed

```
$ sudo docker run hello-world
```
You should see how _Docker_ is downloading an image called [hello-world:latest](https://hub.docker.com/_/hello-world) and runs it.

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete 
Digest: sha256:7e02330c713f93b1d3e4c5003350d0dbe215ca269dd1d84a4abc577908344b30
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
## Section complete....

After this we have installed Docker and tested that it is running correctly. Now we can [continue with this Demo/Lab](../01-Run/README.md).

