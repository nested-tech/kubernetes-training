## Terminology

Some of the basics to get you started.

### Cluster
Automates the distribution and scheduling of application containers. Consists of:
- Master
- Nodes -> Pods -> Containers

### Master
Manages all Nodes within the Cluster.

### Node
A worker machine (run on a physical or virtual machine), onto which pods can be scheduled.

### Pods
A group of containers. It is the basic unit that Kubernetes deals with.

### Service
A service defines a set of pods and a means by which to access them, such as single stable IP address and corresponding DNS name.

### Minikube
A tool that makes it easy to run Kubernetes locally. It runs a single-node Kubernetes cluster inside a VM on your laptop. Supports the majority of Kubernetes features. For more help see the guide [here](https://kubernetes.io/docs/setup/minikube/)