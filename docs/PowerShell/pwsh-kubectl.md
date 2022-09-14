---
sidebar_position: 1
---

# Automate Kubectl with PowerShell

You can use PowerShell in combination with the `kubectl` CLI tool to automate many operations against a Kubernetes cluster.

* Retrieve a list of all Kubernetes Pods, across all Namespaces in the cluster.
* Use the `--output` parameter to return the results as JSON.
* Use the built-in `ConvertFrom-Json` command in PowerShell to interpret the JSON text as objects.

```
kubectl get pods --all-namespaces --output=json | ConvertFrom-Json
```

Next, assign the resulting objects to a variable and echo the object.

```
$PodList = kubectl get pods --all-namespaces --output=json | ConvertFrom-Json
$PodList
```

Notice that there is an `items` child property, so retrieve that, and reassign the variable.

```
$PodList = $PodList.items
```

How many Pods do you have running on your Kubernetes cluster?

```
$PodList.Count
```

How many Pods are running in each Kubernetes Namespace?

```
$PodList | Group-Object -Property { $PSItem.metadata.namespace }
```

How many Pods have `calico` in their names?

```
$PodList | Where-Object -FilterScript { $PSItem.metadata.name -match 'calico' } | Measure-Object
```

