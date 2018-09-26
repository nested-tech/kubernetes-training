## Turning it off

To clean up our cluster.

    kubectl delete service our-http-app
    kubectl delete deployment our-http-app

To remove the docker images

    docker rmi our-http-app our-http-appe:v2 -f

To stop the Minikube VM

    minikube stop
    eval $(minikube docker-env -u)