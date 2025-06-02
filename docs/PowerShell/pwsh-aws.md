---
sidebar_position: 2
title: AWS PowerShell Automation
---

This page serves to document some useful AWS PowerShell scripts that I've written.

### List Amazon EC2 Instances with EMR Cluster ID and Instance Group

Amazon Elastic Map Reduce (EMR) uses Amazon EC2 instances for its various roles: master nodes, core nodes, and task nodes.
Each EC2 instance managed by EMR has some extra built-in tags that can be used to identify the EMR cluster ID and instance group.

This PowerShell script will list Amazon EC2 instances in the current region, but also specifically obtains the EMR cluster ID and EMR instance group for each EC2 instance.
It also "lifts" the `InstanceID` and `InstanceType` properties from the inner `Instances` property, to make them more easily accessible.
The results of this script will print out the current AWS region's EC2 instance IDs & instance type, along with the EMR cluster ID and instance group.

```pwsh
$EC2InstanceList = Get-EC2Instance -ProfileName <default_or_your_profile_name>

foreach ($EC2Instance in $EC2InstanceList) {
  $EC2Instance | Add-Member -MemberType ScriptProperty -Name EMRClusterInstanceGroup -Value {
    $this.Instances[0].Tags.Find({ $args[0].Key -eq 'aws:elasticmapreduce:instance-group-role' }).Value
  }
  $EC2Instance | Add-Member -MemberType ScriptProperty -Name EMRCluster -Value {
    $this.Instances[0].Tags.Find({ $args[0].Key -eq 'aws:elasticmapreduce:job-flow-id' }).Value
  }
  $EC2Instance | Add-Member -MemberType ScriptProperty -Name InstanceID -Value {
    $this.Instances[0].InstanceID
  }
  $EC2Instance | Add-Member -MemberType ScriptProperty -Name InstanceType -Value {
    $this.Instances[0].InstanceType
  }
}

Remove-Variable -Name EC2Instance

$EC2InstanceList | Format-Table -Property InstanceID, InstanceType, EMRCluster, EMRClusterInstanceGroup
```
