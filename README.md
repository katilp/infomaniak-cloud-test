# Test workflowfor Infomaniak Kubernetes resources

This repository contains Argo workflows tested using Infomaniak Kubernetes resources.

## Prerequisites

### Infomaniak

An Infomaniak account.

Order a cloud product under Cloud computing from https://www.infomaniak.com/

Find the cloud under Cloud Computing -> Public Cloud in https://manager.infomaniak.com/
and create a project.

Create a Kubernetes cluster and add the node (instance) pool.

### Your terminal

`kubectl` installed, see https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

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

## Storage

### Your terminal

Install the tools to interact with the storage

```
pip install python-openstackclient python-swiftclient
```

### S3 object storage

Download the OpenStackRC file from the Infomaniak project view.

Source it in your terminal with 

```
source <YOUR-PROJECT-NAME>-openrc.txt
```

Create an object storage with

```
openstack container create mystorage
```

Create S3 credentials with

```
openstack ec2 credentials create
```

You will need the values of `access` and `secret` fields in what follows. 


### Storage access in the cluster

In your terminal, create the cluster secrets to access the storage with

```
kubectl create secret generic s3-credentials \
  --from-literal=AWS_ACCESS_KEY_ID='<the value of the access field>' \
  --from-literal=AWS_SECRET_ACCESS_KEY='<the value of the secret field>' \
  -n argo
```



## Workflow examples

In the subdirectories. 
