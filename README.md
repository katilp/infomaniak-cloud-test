# Test workflow for Infomaniak Kubernetes resources

This repository contains Argo workflows tested in Infomaniak Kubernetes resources.

## Prerequisites

An Infomaniak account, and a Kubernetes cluster on Infomaniak resources.

`kubectl` installed.

Kubeconfig file downloaded from Cluster Kubernetes view of https://manager.infomaniak.com
and exported as `KUBECONFIG`, or saved in a default location. 

Check the connection with

```
kubectl cluster-info
```


## Argo workflows

See: https://github.com/argoproj/argo-workflows/releases/

Create a namespace

```
kubectl create ns argo
```

Argo workflows controller and server can be set up in an existing cluster with

```
kubectl apply -n argo --server-side -f https://github.com/argoproj/argo-workflows/releases/download/v4.0.1/install.yaml
```

A service account and its roles and bindings can be deployed with

```
kubectl apply -f manifests/
``` 

Check the resources with

```
kubectl get all -n argo
```

The Argo CLI to submit jobs from the terminal can be installed with

```
curl -sLO "https://github.com/argoproj/argo-workflows/releases/download/v4.0.1/argo-linux-amd64.gz"
gunzip "argo-linux-amd64.gz"
chmod +x "argo-linux-amd64"
sudo mv "./argo-linux-amd64" /usr/local/bin/argo
```

## Workflow examples

In the subdirectories. 
