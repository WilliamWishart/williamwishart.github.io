---
layout: post
title: "How to create deployment with kubectl"
date: 2021-01-30
categories: Reference
---

# Problem

You want to create a deployment with one or more containers on a Kubernetes cluster.

From [Hello Minikube][minikube-create-deployment]

> A Kubernetes Pod is a group of one or more Containers, tied together for the purposes of administration and networking. The Pod in this tutorial has only one Container. A Kubernetes Deployment checks on the health of your Pod and restarts the Pod's Container if it terminates. Deployments are the recommended way to manage the creation and scaling of Pods.

# How to create a deployment for one Container

First, make sure we are working with the correct namespace.

```Bash
kubectl config set-context --current --namespace=my-namespace
```

Where my-namespace is the name of your namespace.

Check that we have switched to the required namespace.

```bash
kubectl config view | grep namespace:
```


Use the kubectl create command to create a Deployment that manages a Pod. The Pod runs a Container based on the provided Docker image.

```Bash
kubectl create deployment hello-node --image=k8s.gcr.io/echoserver:1.4
```

[minikube-create-deployment]: https://kubernetes.io/docs/tutorials/hello-minikube/
[cheatsheet]: https://kubernetes.io/docs/reference/kubectl/cheatsheet/