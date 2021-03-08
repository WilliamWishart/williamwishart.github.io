---
layout: post
title: "How to create a Helm Chart"
date: 2021-01-30
categories: Reference
---

# Problem

You want to create a helm chart.

# Create a manual deployment

Create a new folder for the Helm Chart - note that the folder name must reflect the chart name.
CD into the new folder and create a new file called Chart.yaml.

This file could look like the follow

```yml
apiVersion: v1
name: my-nginx
version: 0.1.0
appVersion: 1.0
description: This is a Helm example using Nginx
```

Create the deployment yaml from a create deploy dry run, outout to yaml and piped to the deployment.yaml file in the templates folder

```bash
$ kubectl create deploy my-nginx --image nginx --dry-run -o yaml > templates/deployment.yaml
```

Install the Chart from the current folder by running the following command.

```bash
$ helm install my-test .
```

Where my-test is the name for the deployment, this can be anything that makes it easy to identify the deployment.

Now check the Helm package is available with the following

```bash
$ helm list
```

Check the chart deployment is up and running by

```bash
$ kubectl get all
```

# Add a Service and Upgrade

```bash
$kubectl expose deploy my-nginx --port 80 --dry-run -o yaml > templates/service.yaml
```

Update the Chart.yaml version from 0.1.0 to 0.2.0

```bash
helm upgrade my-test .
```

# Rollback

# Remove the Helm Deployment

```bash
helm delete my-test
```
