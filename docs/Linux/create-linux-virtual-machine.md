# Create Linux Virtual Machine

In this guide, you'll learn how to create a Linux virtual machine.
You can create and destroy Linux virtual machines on cloud providers or on your local development workstation.

## Cloud Providers for Linux Virtual Machines

There are lots of different cloud providers that enable you to create Linux virtual machines.
I'll list some of the more common ones here, but keep in mind that you are welcome to use any cloud provider that you wish.

| Cloud Vendor                | Description                                                                                                                                   |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Digital Ocean               | Publicly traded company that provides managed services, including Linux virtual machines (aka. "Droplets")                                    |
| Linode                      | Company owned by Akamai that offers managed services, including Linux virtual machines (aka. "Linodes")                                       |
| Amazon Web Services (AWS)   | One of the earliest cloud vendors, providing a massive portfolio of managed services, including Linux virtual machines (aka. "EC2 instances") |
| Microsoft Azure             | Major competitor to AWS,provides large portfolio of managed services, including Linux virtual machines                                        |
| Google Cloud Platform (GCP) | Google's public cloud platform, providing a large portfolio of managed services, including Linux virtual machines                             |
| Scaleway                    | European public cloud platform that provides managed services, including Linux virtual machines                                               |
| Vultr                       | public cloud platform that is very easy to use, similar to digital ocean or Linode. Enables deployment of Linux virtual machines              |


## Local Tools to Create Linux VM

You can use any of these tools to create Linux virtual machines on your local development system.
Some tools can be used cross-platform, while others are specific to certain operating systems.

| Name                                                         | Description                                                                                                  | Platforms             |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | --------------------- |
| [Multipass](https://multipass.run)                           | Open source, cross-platform tool from Canonical, that easily creates Ubuntu Linux virtual machines           | Linux, MacOS, Windows |
| [UTM](https://github.com/utmapp/UTM)                         | Open source tool for MacOS users, that can easily create Windows & Linux virtual machines from any ISO file  | MacOS                 |
| [VirtualBox](https://www.virtualbox.org/)                    | Open source, cross-platform virtualization tool to create Windows & Linux virtual machines                   | Linux, MacOS, Windows |
| [Vagrant](https://www.vagrantup.com/)                        | Open source, cross-platform CLI tool from Hashicorp that allows you to define virtual machines as code files | Linux, MacOS, Windows |
| [Hyper-V](https://learn.microsoft.com/en-us/virtualization/) | The hypervisor that's built into the Windows platform. Install any guest operating system.                   | Windows               |