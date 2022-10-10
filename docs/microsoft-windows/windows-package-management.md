# Automate Package Management on Microsoft Windows

## Why Use a Windows Package Manager?

When you set up a new Windows system, it typically takes a long time to install software packages.
The manual process requires visiting a variety of websites in your browser, downloading the software packages individually, and then running through graphical installers.
Additionally, you must manually update these packages over time, and many applications don't have built-in auto-updaters.
This manual installation and updating process is onerous, and could be greatly simplified.

By using a command line package manager, you can greatly simplify the process of installing packages on a fresh Windows system.
You also gain the simplification of updating software packages, as you don't have to navigate different websites manually, for each package.
Command line package managers can be scheduled to run inside Windows Task Scheduler, to automatically update packages periodically (ie. daily, weekly).

## About Windows Package Managers

You can install, update, and remove software package on the Microsoft Windows platform using command line automation tools.
There are several different tools available.

* [Scoop](https://scoop.sh/)
* [Winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/)
* [Chocolatey](https://chocolatey.org/)

## Scoop

The Scoop package manage is an open source, community-supported project.
Many popular software development tools are available for Scoop.
You can install the Scoop package manager with a single command, using PowerShell.

```pwsh
irm get.scoop.sh | iex
```

### Install Git Package with Scoop

Once Scoop has been installed on your system, you can install software package with it.
One of the most important software packages you'll need is Git.
You'll need to install Git in order to add other Scoop buckets.
This happens because Scoop package metadata is stored in Git repositories on GitHub.

```pwsh
scoop install git
```

### Add Buckets to Scoop

Once you've installed the Git package via Scoop, you can add other Scoop "buckets."
Buckets contain the metadata for Scoop packages, which allows you to search for and install them.
For example, to install the ["extras" bucket](https://github.com/ScoopInstaller/Extras), which contains many popular applications, you can run the command below.

```pwsh
scoop bucket add extras
```

### Popular Scoop Packages

Some of the popular software development tools that you might need to install with the scoop package manager include the following.

| Name                         | Description                                                                                        | Install Command               |
| ---------------------------- | -------------------------------------------------------------------------------------------------- | ----------------------------- |
| Microsoft Visual Studio Code | Open source, cross-platform text editor for software developers                                    | scoop install extras/vscode   |
| Hashicorp Terraform          | Open source, cross-platform automation tool to deploy multi-cloud infrastructure resources         | scoop install main/terraform  |
| WinSCP                       | Open source SCP/SFTP/FTP GUI for Windows                                                           | scoop install extras/winscp   |
| kubectl                      | The official Kubernetes command line client to manage cluster resources                            | scoop install main/kubectl    |
| OpenLens                     | Open source GUI for managing Kubernetes resources                                                  | scoop install extras/openlens |
| Mockoon                      | Open source, cross-platform GUI for REST API mocking                                               | scoop install extras/mockoon  |
| AWS CLI Tool                 | Cross-platform tool to manage cloud resources on Amazon Web Services (AWS)                         | scoop install main/aws        |
| Azure CLI Tool               | Cross-platform CLI tool to manage cloud resources on Microsoft Azure                               | scoop install main/azure-cli  |
| FFmpeg                       | Powerful, cross-platform CLI tool for managing audio/video files                                   | scoop install main/ffmpeg     |
| Helm                         | Package management tool for deploying apps to Kubernetes clusters                                  | scoop install main/helm       |
| ILSpy                        | GUI tool for .NET decompilation, inspect .NET libraries                                            | scoop install extras/ilspy    |
| MySQL                        | Install the MySQL CLI and optional server binaries (msyqld)                                        | scoop install main/mysql      |
| yt-dlp                       | Command line tool to download videos from sites like YouTube                                       | scoop install main/yt-dlp     |
| Rclone                       | Open source CLI to copy/sync files across many storage providers (ie. local filesystem, Amazon S3) | scoop install main/rclone     |
| Redis                        | Open source, high-performance key-value storage                                                    | scoop install main/redis      |
| scrcpy                       | Remote control tool for Android devices                                                            | scoop install main/scrcpy     |
| Caddy                        | Web server and reverse proxy, very easy to use & configure                                         | scoop install main/caddy      |
| Draw.io                      | Open source, cross-platform GUI tool for building complex cloud / network / generic diagrams       | scoop install extras/draw.io  |
| DBeaver                      | Open-source "community edition" GUI tool for managing databases (MySQL, Postgres, MongoDB, etc.)   | scoop install extras/dbeaver  |
| Telegraf                     | Open source, cross-platform metrics gathering agent from InfluxData                                | scoop install main/telegraf   |
| Postman                      | Freeware REST API client GUI for testing APIs                                                      | scoop install extras/postman  |
| Rufus                        | Open source tool for easily flashing bootable USB drives with operating system images              | scoop install extras/rufus    |