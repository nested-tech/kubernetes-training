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