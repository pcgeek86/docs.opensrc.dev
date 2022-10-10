# Docker Intro

If you're brand new to Docker, this is a great place to get started.
We'll run through a few core commands that you should remember in order to be effective with Docker.

## Prerequisites

In order to follow this tutorial, the only thing you need is a Linux virtual machine.
There are lots of different tools and cloud services that you can use to obtain a Linux VM.

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

