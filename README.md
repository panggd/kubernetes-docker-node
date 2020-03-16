# kubernetes-docker-node

## Overview
This is a learner project to understand how Kubernetes deploy and manage docker containers.

1. Create a Dockerfile to dockerize a simple ExpressJS app.
2. Create two Kubernetes scripts - deployment.yml and service.yml
3. Install minikube and kubectl
4. Start minikube
5. Build the docker image
6. Run the Kubernetes scripts using kubectl
7. Expose app using Minikube

## Tech stack
- Docker
- Kubernetes
- Minikube
- Kubectl
- ExpressJS

## app
This folder consists of a Dockerfile that pull a Node docker image, npm install an ExpressJS app.

## kube
This folder consists of a deployment.yml and a service.yml.

**deployment.yml** - This file describe how to deploy the docker image, how many instance to deploy, the necessary ports to expose.

**service.yml** - This file describe how to expose the app as a service, similar to the concept of microservice.

## Prerequsites

### Download and install Docker. Follow the below guides.
https://docs.docker.com/install

### Install kubectl and minikube. Follow the below guides.
https://kubernetes.io/docs/tasks/tools/install-minikube
https://kubernetes.io/docs/tasks/tools/install-kubectl


## How to run

### Start Docker daemon
This really depend on your OS. I use Docker for Mac, so it is simply starting the Docker app.

### Start Minikube
Read https://stackoverflow.com/questions/42564058/how-to-use-local-docker-images-with-minikube
```bash
minikube start --driver=docker
eval $(minikube docker-env) #this is to allow pulling of local docker image.
```

### Build the docker image
```bash
docker-compose build --force-rm --no-cache # for a clean build
```

### Run kubectl to deploy the docker containers
```bash
kubectl apply -f kube
kubectl get all
```

### Expose the service
```bash
minikube service app-express
```

## Housekeeping
Here are some housekeeping tips if you are on a low memory resource machine like me.

```bash
# This is to have a clean state of your docker environment
docker stop $(docker ps -a -q) && \
docker container prune && \
docker volume prune && \
docker network prune && \
docker image prune

# kubectl housekeeping
kubectl delete deployment <deployment-name>
kubectl delete service <deployment-name>

# minikube housekeeping
minikube stop
minikube delete
```