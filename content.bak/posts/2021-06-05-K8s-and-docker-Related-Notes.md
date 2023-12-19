---
title: K8s and docker Related Notes
date: 2021-06-05 15:08:29
<<<<<<< HEAD
categories: 
- Notes
tags:
- K8s
- Docker
- en
---

#### 1. Management tools for clusters, pods, deployments, etc. : 
=======
categories:
- Notes
- En
tags:
- K8s
- Docker
---

#### 1. Management tools for clusters, pods, deployments, etc. :
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59

k9s

#### 2. When not able to delete resources in k8s:

First edit resource:

<<<<<<< HEAD
```
=======
``` shell
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
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
<<<<<<< HEAD

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
