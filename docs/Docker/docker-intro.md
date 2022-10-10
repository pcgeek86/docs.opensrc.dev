# Docker Intro

## Learning Objective

If you're brand new to Docker, this is a great place to get started.
We'll run through a few core commands that you should remember in order to be effective with Docker.
After following this guide, you should know how to perform the following tasks:

* Install Docker Engine on Linux
* Download different container image versions from registries
* Run containers
* Attach and detach from containers
* Destroy containers

## Prerequisites

In order to follow this tutorial, the only thing you need is a Linux virtual machine.
There are lots of different tools and cloud services that you can use to [create a Linux VM](Linux/create-linux-virtual-machine.md).
Once you've created your Linux virtual machine, SSH into it to get a shell, and follow this tutorial.

## Container Images and Registries

Containers are created from container *images*, which are most commonly stored in a container registry.
A container image is *kind of* like an operating system image, however containers and operating systems are different concepts.

Some examples of container image registries include [Docker Hub](https://hub.docker.com), [Quay.io](https://quay.io), [Amazon ECR Public](https://gallery.ecr.aws/), and others.
Container images can also be stored on the local filesystem as archive files (`.tar.gz`) and imported into the Docker engine.

There are many container images that contain pre-packaged applications or programming runtimes, like MySQL, MongoDB, Python, PowerShell, Java, and others.

## Install Docker Engine

### Install Docker on Ubuntu Linux

We need to install the Docker Engine on Linux. I typically use Ubuntu Linux because it's well-supported and generally easy to use.
You can install Docker on pretty much any Linux distribution, however.
Ubuntu Linux is based on Debian Linux, and therefore uses the [`apt` package manager](https://help.ubuntu.com/community/AptGet/Howto).
Before you can install packages with `apt`, you need to update the package metadata, using the `update` sub-command.
The `apt upgrade` command will ensure that all pre-installed packages are up-to-date, before we install any additional software.

:::note Sudo Not Required as Root
If you're logged into your Linux system as the root user, you don't need to prefix these commands with `sudo`.
:::

```
sudo apt update
sudo apt ugprade --yes
sudo apt install docker.io --yes
```

The Docker service should automatically be started up once the Docker engine has been installed.
Because Ubuntu Linux uses the `systemd` service manager, you can use the `systemctl` command to query the status of the Docker engine.

```
systemctl status docker
```

### Install Docker on Alpine Linux

Alpine Linux is a lighter weight Linux distribution that is useful for running container-based applications.
Installing the Docker engine on Alpine Linux is incredibly easy, using the [`apk` (Alpine Package Keeper) package manager](https://wiki.alpinelinux.org/wiki/Alpine_Package_Keeper).

On Alpine Linux, the Docker service/daemon is **not** automatically started up after installation, so go ahead and start it with the `service` command.

```
apk add docker
service docker start
```

## Download Container Images

You can download container images from a registry without having to run a container.
You accomplish this by using the `pull` command.
Once the container image has been downloaded / cached onto your Linux system's filesystem, you can run containers from it.

For starters, why not try downloading the container image for Alpine Linux?

```
docker pull alpine
```

You could also download the container image to run a Python container.

```
docker pull python
```

### Use a Different Registry

By default, the Docker Engine assumes that you want to download container images from the Docker Hub (`docker.io`).
The commands above are equivalent to the commands below.

```
docker pull docker.io/alpine
docker pull docker.io/python
```

If you want to pull a container image from a different registry, you simply prefix the container image name with the registry's DNS name.
For example, if you want to download [Prometheus](https://prometheus.io/) from the Quay.io registry, use the command below.

```
docker pull quay.io/prometheus/prometheus
```

### Container Image Tags

Container images can define multiple "tags."
These tags are most commonly used to define different versions of a software package.
However, developers can use any image tagging strategy that they want to.

By default, the Docker engine uses the `latest` tag.
If you want to download a specific container image version you can specify the tag after the container image name.
Container image registries list the different tags that are available for each image.

For example, if you want to download a specific version of the Python runtime, from Docker Hub, use the following command.
Visit the [Python page](https://hub.docker.com/_/python) on Docker Hub to find other tags that are available.

```
docker pull python:3.10.7
```

## Run Containers with Docker

Now that you've learned the basics about container images, let's actually run some containers.
We use container images to launch containers from.
One of the major benefits of this model is that any data created by your application will be layered on top of the base image.
If you run multiple containers from the *same* image, then you *avoid* duplicating the data from the base image.
The net result is that containers use only the disk space that they actually need.

NGINX is a popular web server that is easy to deploy as a container.

```
docker run nginx
```

Press `CTRL + C` to return back to your shell.
When you press `CTRL + C`, Docker sends a `SIGINT` termination signal to the container's process.
The process (NGNIX, in this case) has an opportunity to perform cleanup tasks before it exits.

```
^C2022/10/10 14:09:08 [notice] 1#1: signal 2 (SIGINT) received, exiting
2022/10/10 14:09:08 [notice] 30#30: exiting
2022/10/10 14:09:08 [notice] 30#30: exit
2022/10/10 14:09:08 [notice] 1#1: signal 14 (SIGALRM) received
2022/10/10 14:09:08 [notice] 1#1: signal 17 (SIGCHLD) received from 30
2022/10/10 14:09:08 [notice] 1#1: worker process 30 exited with code 0
2022/10/10 14:09:08 [notice] 1#1: exit
```

### Run Detached Container

With the previous command, you'll see that logs from the web server are printed out to the terminal, and the Docker CLI remains attached to the container.
Typically you want to run container services, like the NGINX web server, in the background, so that you can continue to work in your shell.
This is easy to accomplish by running a container in the "detached" state.
By running a container in the detached state, you will retain control over your shell session.

```
docker run --detach nginx
```

When you run a container in detached state, Docker will print out the container the new container's ID.
You can use this container ID to run additional management commands against the container, such as destroying it.

### Interact with Containers

While production applications typically run as background services, and don't allow direct interaction, you can actually spin up containers that are interactive.
This is extremely helpful if you are learning, exploring, developing code, or just experimenting with ideas.
Use the `--interactive` and `--tty` parameters together, to make the container interactive.

```
docker run --interactive --tty python
```

Press `CTRL + D` to exit, or type `exit()` at the Python prompt, to return back to your Linux VM.

### Detach From and Attach To Containers

If you want to leave an interactive container running, but return back to your Linux VM's shell, you can **detach** from a container.
Later on, you can attach to the container that you previously detached from.

Go ahead and run another interactive container to start.

```
docker run --interactive --tty python
```

This time, instead of exiting the container, press `CTRL + P` immediately followed by `CTRL + Q`.
This will detach Docker CLI from the running container, but will *leave the container running*.

You can verify that the container is still running by using the following command.

```
docker ps
```

If you'd like to attach to the container that you just detached from, use the `docker attach` command.
The previous command shows the container ID and name. You can use either one to attach.
If you use the container ID, you don't need to type the entire ID, however you do need to use the full name if you specify the name instead of the ID.

```
docker attach b8c
```

### Terminate Containers with Docker

If you've left a container running, but want to destroy it, use the `docker rm` command.
Similar to the `docker attach` command, you can specify the container name or partial ID, to destroy it.

```
docker run nginx
docker rm b8c
```

