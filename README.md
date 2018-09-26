# kubernetes-training
A small subset of the infrastructures functionality for learning how to manage containers.

## Starting with Docker

First we will build and run a docker image.

Inside the `application` folder run the below steps:
1. `npm run image:build`
2. `npm run image:run`
3. In a browser open http://localhost:3000

Once you have verified it has worked you can stop the image with
1. `docker ps`
2. `docker stop <our container id>`

## Installing Kubernetes and Minikube

We will now build and interact with our cluster using the `kubectl` CLI client and `Minikube`.

Move back to the root folder.

Install the Kubernetes client 

    brew install kubectl 

Install our Minikube client

    brew cask install minikube

## Building and deploying your cluster 

    minikube start

This command creates and configures a virtual machine that runs a single-node Kubernetes cluster. It also configures your kubectl installation to communicate with this cluster under the context `minikube`.

    minikube dashboard

Opens your Kubernetes dashboard in a browser.

As Minikube VM uses its own Docker host we have to enable the Minikube Docker daemon and then rebuild our docker iamge so it is available for Minikube.
        
    eval $(minikube docker-env)

Now go and rebuild your Docker image. It should appear if you check (`docker images`)

Now lets run a Pod with our Docker image in and create a Deplyoment to manage that Pod. `--image-pull-policy=Never` so we always use the local image rather than pulling from a registry.

    kubectl run our-http-app --image=our-http-app-image --port=3000 --image-pull-policy=Never

We can view our Deployment with

    kubectl get deployments

We can view our Pod with 
    
    kubectl get pods

You can see the Deployment status inside the Kubernetes Dashboard.

We need to make our Pod conainer accessible from outside the Kubernetes virtual network. We do this via exposing the Pod as a service. The `-type=LoadBalancer` flag indicates that we want to expose our Service outside of the cluster.

    kubectl expose deployment our-http-app --type=LoadBalancer

View services with

    kubectl get services

Minikube requires we make `LoadBalancer` types available via the `service` command

    minikube service our-http-app

This will expose it and open the bwoser window onto the local IP that serves your application.

## To update and re-Deploy

If you have made an update and want that Deployed.

After your change build your image again, possibly under a new version (perhaps append `:v2` to the end of the docker image name).
Update the image of the Deployment
    
    kubectl set image deployment/our-http-app our-http-app=our-http-app:v2

Then run the `service` command again.

    minikube service our-http-app

## Turning it off

To clean up our cluster.

    kubectl delete service our-http-app
    kubectl delete deployment our-http-app

To remove the docker images

    docker rmi our-http-app our-http-appe:v2 -f

To stop the Minikube VM

    minikube stop
    eval $(minikube docker-env -u)

## Terminology

Some of the basics to get you started.

### Pods
A group of containers. It is the basic unit that Kubernetes deals with.

### Node
A physical or virtual machine running Kubernetes, onto which pods can be scheduled.

### Service
A service defines a set of pods and a means by which to access them, such as single stable IP address and corresponding DNS name.

### Minikube
A tool that makes it easy to run Kubernetes locally. It runs a single-node Kubernetes cluster inside a VM on your laptop. Supports the majority of Kubernetes features. For more help see the guide [here](https://kubernetes.io/docs/setup/minikube/)