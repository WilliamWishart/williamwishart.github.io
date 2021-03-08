---
layout: post
title: "Setup Kubernetes on Docker for Mac"
date: 2021-02-22
categories: Reference
---

## Setup Docker Image Registry

### In Docker

Outline the steps needed to setup kubernetes in docker and how to deploy the docker registry in there. There was an issue using localhost so used kubernetes.docker.internal instead. This needed a change to the etc/hosts file.

### In Kubernetes

Outline the steps needed to setup kubernetes in docker and how to deploy the docker registry in there. There was an issue using localhost so used kubernetes.docker.internal instead. This needed a change to the etc/hosts file.

### In Minikube

Outline the steps needed to setup kubernetes in docker and how to deploy the docker registry in there. There was an issue using localhost so used kubernetes.docker.internal instead. This needed a change to the etc/hosts file.

## Push local image to Docker Image Registry in Kubernetes

Build a new docker image

    docker build --tag=simpleubuntu .

Tag that image with the name of the target registry. In some cases this can be localhost, but where that fails, you will want to use a fake domain path.

    docker tag simpleubuntu localhost:5000/simpleubuntu

Request a catalog from the registry. If this is the first call, it will return an empty list.

    curl -X GET http://localhost:5000/v2/\_catalog

Docker push that taged image to the registry.

    docker push localhost:5000/simpleubuntu

Check the image was pushed to the registry.

    curl -X GET http://localhost:5000/v2/\_catalog

Now you can remove the original image from Docker images

    docker images
    docker image remove localhost:5000/simpleubuntu
    docker images

Attempt to run the image from the local registry.

    docker run --detach --publish=5001:80\ --name=simpleubuntu simpleubuntu

kubectl config set-context --current --namespace=dev
eval $(minikube -p minikube docker-env)  
kubectl create -f hello-world.yml

helm install hello-world .
helm uninstall hello-world

Potential solution that will allow minikube to talk to the docker reg

https://hasura.io/blog/sharing-a-local-registry-for-minikube-37c7240d0615/

    kubectl port-forward --namespace kube-system \ $(kubectl get po -n kube-system | grep kube-registry-v0 | \awk '{print $1;}') 5000:5000

    kubectl port-forward --namespace kube-system kube-registry-v0-lgtgs 5000:5000

Kubernetes Dashboard for use with kubernetes running on docker

https://github.com/kubernetes/dashboard/releases

Use this link to proxy into the dashboard

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

Get new token

    kubectl -n kubernetes-dashboard get secret $(kubectl -n kubernetes-dashboard get sa/admin-user -o jsonpath="{.secrets[0].name}") -o go-template="{{.data.token | base64decode}}"

How to use local docker images with Minikube

https://stackoverflow.com/questions/42564058/how-to-use-local-docker-images-with-minikube

nginx http server hello world

https://bartek-blog.github.io/nginx/node/javascript/2019/12/15/nginx-hello-world.html

### Setup Ingress Controller

    kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.44.0/deploy/static/provider/cloud/deploy.yaml
