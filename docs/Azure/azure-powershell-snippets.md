# Azure PowerShell Snippets

On this page we will take a look at some code snippets for the Azure PowerShell module.

### Install Azure PowerShell

```pwsh
Install-Module -Name Az -Scope CurrentUser -Force
```

### Find Azure Regions (Locations)

If you need to discover which Azure Regions are available, use this command:

```pwsh
Get-AzLocation | Format-Table -AutoSize -Property DisplayName, Location, PhysicalLocation, RegionType
```

### Create an Azure Resource Group

```pwsh
$ResourceGroup = @{
    Name = 'trevor01'
    Location = 'westcentralus'
}
New-AzResourceGroup @ResourceGroup
```

## Azure Container Instance

Make sure the Resource Provider is registered first:

```pwsh
Register-AzResourceProvider -ProviderNamespace Microsoft.ContainerInstance
```

Then you use a few commands to configure the Container Instance resource. 
This example exposes two ports: 80 and 443. You can add more ports or change them if you'd like to.
You can also deploy container images from any public registry, such as [Amazon ECR Public](https://gallery.ecr.aws/).

```pwsh
$Port = New-AzContainerInstancePortObject -Port 80 -Protocol TCP
$Port2 = New-AzContainerInstancePortObject -Port 443 -Protocol TCP
$Container = New-AzContainerInstanceObject -Image docker.io/nginx -Name nginx -Port @($Port, $Port2) -RequestCpu 1 -RequestMemoryInGb 0.5
$ContainerGroup = @{
    ResourceGroupName = 'trevor01'
    Location = 'westcentralus'
    Container = $Container
    Name = 'nginx'
    IPAddressDnsNameLabel = (New-Guid).Guid.Replace('-', '')
    OSType = 'Linux'
    RestartPolicy = 'Always'
    IPAddressType = 'Public'
}
New-AzContainerGroup @ContainerGroup
```

### Delete Azure Container Instance

You can delete an Azure Container Instance resource, from the specified Resource Group, with this command:

```pwsh
$Params = @{
  Name = 'nginx'
  ResourceGroupName = 'trevor01'
}
Remove-AzContainerGroup @Params
```

### Create an Azure Storage Account

Many of these Storage Account parameters are optional, as default values will be used instead.

```pwsh
$StorageAccount = @{
    Name = 'trevor999999' -f $Prefix
    ResourceGroupName = $ResourceGroup.Name
    Location = 'westcentralus'
    SkuName = 'Standard_LRS'
    Kind = 'StorageV2'
    AccessTier = 'Hot'
    EnableHttpsTrafficOnly = $true
    AllowBlobPublicAccess = $false
    MinimumTlsVersion = 'TLS1_2'
    AllowSharedKeyAccess = $true
    PublicNetworkAccess = 'Enabled'
}
New-AzStorageAccount @StorageAccount
```

Potential Errors:

```
Feature MinimumTlsVersion 1.3 is not supported.
Cannot validate argument on parameter 'MinimumTlsVersion'. The argument "TLS1_5" does not belong to the set "TLS1_0,TLS1_1,TLS1_2,TLS1_3" specified by the ValidateSet attribute.
```
