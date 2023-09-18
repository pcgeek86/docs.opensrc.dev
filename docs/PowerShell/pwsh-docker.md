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

Now that you know how to run PowerShell by itself inside a Linux container, it's time to build your own, custom image.
You'll use the `docker build` command to invoke the build process, but first we need an instruction file.
The instruction file is a simple text file called `Dockerfile`.
You can technically use a different file name, but this is the default that Docker Engine looks for, in your project directory.

### Set Base Container Image

Let's start from the top. The first thing we need to do is tell Docker to begin with the PowerShell image as the "base."
Any additional instructions will build upon the PowerShell base, so we don't have to install PowerShell ourselves.
The `FROM` instruction is what indicates the base image you want to use.

```
FROM mcr.microsoft.com/powershell
```

### Inject Script File

Next, we need to inject a custom script file into the container image.
For the sake of example, let's say that you have a script file called `myscript.ps1`.
We need to copy this script from the project directory (aka. Docker build context) into the new container image.

By convention, I typically place code into the `/data` directory in the container filesystem.
You're welcome to use any alternative directory structure that you prefer, however.

The `WORKDIR` instruction tells Docker to set the current working directory to the specified path.
If the directory doesn't already exist, Docker will create it for you.

We'll use the `ADD` instruction to copy the `myscript.ps1` file from the same directory as `Dockerfile`, and place it into `/data`.
The last argument is the destination directory, and the preceding arguments are the individual paths that you want to copy into the new container image.

```
WORKDIR /data
ADD ["myscript.ps1", "/data/"]
```

Now your script file will be embedded into the new container image, when you run a build!

### Set Container Image Entrypoint

You could run a container image build at this point, but generally, container images include a custom entrypoint.
Previously, we saw how running the PowerShell base image runs an interactive PowerShell session.
However, we want to *modify* this behavior to make your custom script the entrypoint instead.

Using the `ENTRYPOINT` instruction, we can tell Docker Engine to set a specific command as the entrypoint
to our custom container image.
This instruction simply accepts a JSON array of input arguments.
The PowerShell binary, named `pwsh`, provides the `-File` parameter, which enables us to directly invoke a script file,
instead of entering an interactive session.

```
ENTRYPOINT ["pwsh", "-Command", "/data/myscript.ps1"]
```

Since the `WORKDIR` has already been set to `/data`, you don't *have* to include the `/data/` prefix to `myscript.ps1`.
However, I generally prefer to be more explicit, rather than rely on environmental settings.

### Run Container Image Build

You're finally ready to run a container image build!

From your project directory, containing the `Dockerfile` and `myscript.ps1`, run the command below.

```
docker build --tag mypwsh .
```

The period at the end just indicates the "current directory" as the build context that's sent to the Docker Engine for processing.
After the build process completes, you should be able to find your custom, tagged container image by running the following command.

```
docker image ls
```

If you don't see `mypwsh` in the list of local container images, then you most likely encountered an error during the build.

### Test Your Custom Container Image

Now that you've built a custom container image on top of the PowerShell base, let's test it out!
We'll add a new argument `--rm` to the Docker CLI, that automatically removes the container after it exits.
This helps prevent lots of outdated, stopped containers from clogging up your Docker Engine.

Run this command to see the results of your script:

```
docker run --rm -it mypwsh
```

If the command hangs, you can use `CTRL + C` to abort execution of PowerShell, and the container.

## Conclusion

At this point, you should have successfully built your own custom container image on top of PowerShell!
If you want to explore beyond this, like installing PowerShell modules into your custom image, check out the `RUN` instruction.
Using `RUN`, you can execute arbitrary commands in your container image build, such as installing modules, so that your script
has all of its dependencies available as soon as it starts.

If you run into issues, feel free to reach out to me on social media channels, and I'll see if I can help you!