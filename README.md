# kubernetes-training
A small subset of the infrastructures code for learning how to manage containers.

### Getting started with Docker

First we will build and run a docker image.

Inside the `application` folder run the below steps:
1. `npm run image:build`
2. `npm run image:run`
3. In a browser open http://localhost:3000

Once you have verified it has worked you can stop the image with
1. `docker ps`
2. `docker stop <our container id>`

### Using Kubernetes and Minikube

We will now build and interact with our cluster using the `kubectl` CLI client and `Minikube`.

Install the Kubernetes client 

    brew install kubectl 

Install our Minikube client

    brew cask install minikube



## Terminology

Some of the basics to get you started.

### Pods
A group of containers. It is the basic unit that Kubernetes deals with.

### Node
A physical or virtual machine running Kubernetes, onto which pods can be scheduled.

### Service
A service defines a set of pods and a means by which to access them, such as single stable IP address and corresponding DNS name.

### Minikube
A tool that makes it easy to run Kubernetes locally. It runs a single-node Kubernetes cluster inside a VM on your laptop. Supports the majority of Kubernetes features.