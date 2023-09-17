---
title: Run PowerShell Scripts in Docker
---

# Introduction: PowerShell and Docker

If you're writing PowerShell scripts, and are wondering how to deploy and schedule them, then you'll most likely want to consider using Linux containers.
Docker is one of the main projects that enables you to run Linux containers.

There are many benefits to using Linux containers, but one key one is dependency management.
Let's say that you have two PowerShell scripts, and each of them need to use a specific version of a module.
It's possible that you can run into version conflicts between the two modules, which must be resolved manually.
By isolating each PowerShell script, and its dependencies, into separate container images, you ensure that each container environment can't "see" the other.

Automated testing is another great reason to use Docker.
Normally you'd "install" a specific version of PowerShell on your system, and keep it up-to-date.
But what if you need to test a script on an older version of PowerShell, to ensure compatibility, or execute a Pester test suite?
Once again, rather than manually downgrading the PowerShell runtime on a specific system, you can run different PowerShell versions side-by-side with Linux containers, via Docker.

What if you need to scale up your PowerShell script to run more instances of it?
How would you approach solving this challenge?
With Docker, it's easy to simply create more containers, using your custom image that has your script packaged inside it.

Alright, so now that you understand the benefits to using Docker to run your PowerShell scripts, let's take a look at **how** to run PowerShell scripts in containers!

## Install Docker Engine

First of all, you'll need to install the Docker Engine. 
Docker Engine is a background service (daemon) that you interact with using the Docker CLI tool.
Once Docker Engine is installed, you can download the base PowerShell container image, and then build your own custom images.

You can install the Docker Engine on a Linux system using a package manager like `apt`, `zypper`, or `yum`.

### Ubuntu

On the popular Ubuntu Linux operating system, you can use this command to install Docker Engine:

```
sudo apt-get update;
sudo apt-get install docker.io --yes;
```

:::note Permission to Docker Engine
If you're logged into your Linux system as a non-root user, you'll need to use `sudo` to run Docker commands, or add your user account to the `docker` group.
:::

Assuming that your Linux username is `ubuntu`, then you'd use this command to allow your user account access to the Docker Engine.
After running the command, you'll need to exit your shell and re-login, so that the group membership takes effect.


```
sudo usermod --append --groups docker ubuntu
```

Once you're logged back in, you can simply run the `groups` command to display the groups that your user account is a member of.

## Download PowerShell Container Image

Once you've installed the Docker Engine, you'll need to download the base image for PowerShell.
You can download container images for many different versions of PowerShell.
These versions are known as "tags" in the world of containers.

Year ago, Microsoft hosted container images for PowerShell on Docker Hub, but they have since changed to using their own, separate image registry.
The DNS name of the Microsoft container image registry is `mcr.microsoft.com`.
To download the container image for the latest version of PowerShell, you can use the command below.

```
docker pull mcr.microsoft.com/powershell:latest
```

After you've downloaded the container image, you can check which images you have cached locally by using the following command.
You should see `mcr.microsoft.com/powershell:latest` show up in that list.

```
docker image ls
```

If you want to download a container image for a different version of PowerShell, you can find the "tag" name and replace `latest` with it.
[This link](https://mcr.microsoft.com/v2/powershell/tags/list) should contain the list of tags available for PowerShell in a raw JSON response.
For example, to download PowerShell 6.1.0 on Fedora 28, you would use the tag `6.1.0-fedora-28`.

```
docker pull mcr.microsoft.com/powershell:6.1.0-fedora-28
```

## Run PowerShell Container

To run a PowerShell container, that you can interact with, you can use the following command.
The `--interactive` and `--tty` parameters can be shortened to `-it` if you prefer.
Those parameters are necessary to make the container interactive.
By default, Docker runs containers as background services, such as web APIs.

```
docker run --interactive --tty mcr.microsoft.com/powershell:latest
```

Of course, you can replace `latest` with a specific PowerShell container image tag as well.

From the interactive shell, you can run whatever PowerShell commands you want to.
You can exit out of the container by typing `exit` in PowerShell.
This will cause PowerShell itself, and the Docker container, to stop running.

If you want to restart the container, and attach to it interactively, you can use this command:

```
docker ps --all  # Find the unique ID of the container
docker start --interactive --attach <containerID>
```

Congratulations! You've run PowerShell inside a Linux container, without having to "install" it directly onto the operating system.
From here, you can download a PowerShell script using `Invoke-WebRequest`, and then execute it, or install `vim` and write a script directly inside the container filesystem.

## Build Custom Container Image

:::note TODO
This content coming soon!
:::