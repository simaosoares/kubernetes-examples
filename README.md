# Kubernetes Examples

Sample project containing Kubernetes examples

Table of contents:

* [Getting Started](#getting-started)
* [minikube](#minikube)

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
