---
layout: post
title: "How to use local docker images with Minikube?"
date: 2021-01-25
categories: Reference
---

Use a local registry:

    docker run -d -p 5000:5000 --restart=always --name registry registry:2

Now tag your image properly:

    docker tag ubuntu localhost:5000/ubuntu

Note that localhost should be changed to dns name of the machine running registry container.

Now push your image to local registry:

    docker push localhost:5000/ubuntu

You should be able to pull it back:

    docker pull localhost:5000/ubuntu

Now change your yaml file to use local registry.

Think about mounting volume at appropriate location to persist the images on registry.

update:

You'll need to add the local registry as insecure in order to use http (may not apply when using localhost but does apply if using the local hostname)

Don't use http in production, make the effort for securing things up.
