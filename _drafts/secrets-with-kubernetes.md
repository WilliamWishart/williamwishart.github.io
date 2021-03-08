---
layout: post
title: "Using Secrets in Kubernetes"
date: 2021-02-14
categories: Reference
---

Base64 encoding

    echo -n "password" | base64

Where -n will not add a new line character to the output

Will result in

    cGFzc3dvcmQ=

    kubectl create secret generic secret-demo --from-literal=

    kubectl get secrets

Secrets can be setup as `ENV` variables or mounted as a volume within the pod
