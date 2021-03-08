---
layout: post
title: "How to use local docker images with Minikube?"
date: 2021-01-25
categories: Reference
---

docker build --tag=simpleubuntu .

docker tag simpleubuntu localhost:5000/simpleubuntu
curl -X GET http://localhost:5000/v2/\_catalog

docker push localhost:5000/simpleubuntu
curl -X GET http://localhost:5000/v2/\_catalog

docker images
docker image remove localhost:5000/simpleubuntu
docker images

docker run --detach --publish=5001:80\
--name=simpleubuntu simpleubuntu

OR

kubectl config set-context --current --namespace=dev
eval $(minikube -p minikube docker-env)  
kubectl create -f hello-world.yml

helm install hello-world .
helm uninstall hello-world

# Potential solution that will allow minikube to talk to the docker reg

# https://hasura.io/blog/sharing-a-local-registry-for-minikube-37c7240d0615/

https://hasura.io/blog/sharing-a-local-registry-for-minikube-37c7240d0615/


----

Running kubernetes in Docker
Install kubernetes dashboard
https://github.com/kubernetes/dashboard/releases