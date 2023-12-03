---
title: K8s and docker Related Notes
date: 2021-06-05 15:08:29
categories: 
- Notes
tags:
- K8s
- Docker
---

#### 1. Management tools for clusters, pods, deployments, etc. : 

k9s

#### 2. When not able to delete resources in k8s:

First edit resource:

```
kubectl edit <resource name>
```

then delete the `finalizer` part and try again.

#### 3. filtering docker images

```shell
docker image "name*"
```

<!--more-->

#### 4. save and load docker images

```shell
docker image save > smartcity_images
docker image load < smartcity_images
```

#### 5. getting k8s events

```
kubectl get events
```

