# Kubernetes Examples

Sample project containing Kubernetes examples

Table of contents:

* [Getting Started](#getting-started)
* [minikube](#minikube)
* [Basic commands](#basic-commands)
* [Pods](#pods)
* [ReplicaSet](#replicaset)
* [Deployments](#deployments)
  * [Update and Rollback](#update-and-rollback)
* [Services](#services)
* [Setup Multi Node cluster using Kubeadm](#setup-multi-node-cluster-using-kubeadm)

## Getting Started

Some tools to get Kubernetes up and running:

* minikube
* Kubeadm
* MicroK8s

## minikube

Pre requisites:

* kubectl
* Container or virtual machine manager ex: virtualbox

### kubectl

* Install and set up the kubectl tool: https://kubernetes.io/docs/tasks/tools/

### Container or virtual machine manager

While using Minikube with Virtualization technologies, specify the --vm-driver option like this:
```
minikube start --vm-driver=<driver_name>
```

Example of starting minikube for virtualbox:

```
minikube start --driver=virtualbox
```

* Install MiniKube: https://kubernetes.io/docs/tasks/tools/install-minikube/
* Install VirtualBox: https://www.virtualbox.org/wiki/Downloads
* MiniKube Download page for Windows: https://github.com/kubernetes/minikube/releases
* Minikube Tutorial: https://kubernetes.io/docs/tutorials/hello-minikube/
* More about it here: https://kubernetes.io/docs/setup/learning-environment/minikube/#specifying-the-vm-driver
* Install Minikube: https://minikube.sigs.k8s.io/docs/start/

## Basic commands

```
kubectl get nodes
kubectl describe nodes
```

## Pods

```
kubectl run nginx --image=nginx
kubectl create -f pod-definition.yaml
kubectl get pods
kubectl describe pod myapp-pod
kubectl delete pod myapp-pod
```

## ReplicaSet
```
kubectl create -f replicaset.yaml
kubectl get replicaset
kubectl get rs
kubectl describe replicaset
kubectl describe replicaset replicaset-name
kubectl delete replicaset replicaset-name
kubectl edit replicaset replicaset-name
kubectl scale replicaset replicaset-name --replicas=5
```

## Deployments

```
kubectl get deployments
kubectl get deploy
kubectl describe deployment myapp-deployment
kubectl get all
kubectl create deployment httpd-frontend --image=httpd:2.4-alpine --replicas=3
kubectl create -f deployment-1.yaml
kubectl delete deployment myapp-deployment
```

### Update and Rollback

> `RollingUpdate` default strategy type, other option: `Recreate`

**Create**
```
kubectl create -f deployment-definition.yaml
kubectl create -f deployment-definition.yaml --record
```

`--record` records the command used to create the deployment. Can be shown using the `kubectl rollout history` command

**Get**
```
kubectl get deployments
```

**Update**
```
kubectl apply -f deployment-definition.yaml
kubectl set image deployment frontend nginx=nginx:1.9.1 --record
kubectl edit deployment frontend --record
```

`kubectl set image deployment <DEPLOYMENT_NAME> <CONTAINER_NAME>=<IMAGE> --record`

**Status**
```
kubectl rollout status deployment/frontend
kubectl rollout history deployment/frontend
```

**Rollback**
```
kubectl rollout undo deployment/frontend
```

## Services

> `ClusterIp` is the type of the default kubernetes service

> `nodePort` is not mandatory to be defined 

```
kubectl create -f service-definition.yaml
kubectl get services
kubectl get svc
kubectl get pods,svc
kubectl describe service myapp-service 
minikube service myapp-service --url
```

## Setup Multi Node cluster using Kubeadm

This solution is used for setting up a multi-node Kubernetes cluster in a local environment.

### Setup Lab - VirtualBox

Vagrant can be used to quickly get 3 nodes (docker images) up and running: kubemaster, kubenode01 and kubenode02  

* Oracle VirtualBox: https://www.virtualbox.org/
* Vagrant: https://www.vagrantup.com/
* The link to Vagrant file: https://github.com/kodekloudhub/certified-kubernetes-administrator-course
* If you are new to VirtualBox or Vagrant, please follow this pre-requisites course to learn about it: https://www.youtube.com/watch?v=Wvf0mBNGjXY

### Provision cluster using Kubeadm

We need to install a container runtime into each node in the cluster so that Pods can run there.

**Container Runtimes**

* https://kubernetes.io/docs/setup/production-environment/container-runtimes/
* https://github.com/containerd/containerd/blob/main/docs/getting-started.md
* https://docs.docker.com/engine/install/ubuntu/

> While installing docker engine, only `containerd` is required

Do this
```
sudo apt install containerd
```
instead of
```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

Check status
```
systemctl status containerd
```

Identify cgroup driver
```
ps -p 1
```

* Link to kubeadm installation instructions: https://kubernetes.io/docs/setup/independent/install-kubeadm/
* Link to download VM images: http://osboxes.org/
