---
title: K8s and docker Related Notes
date: 2021-06-05
draft: false
garden_tags: ["en", "notes", "k8s", "docker"]
summary: " "
status: "growing"
---

- [1. Management tools for clusters, pods, deployments, etc. :](#1-management-tools-for-clusters-pods-deployments-etc-)
- [2. When not able to delete resources in k8s:](#2-when-not-able-to-delete-resources-in-k8s)
- [3. filtering docker images](#3-filtering-docker-images)
- [4. save and load docker images](#4-save-and-load-docker-images)
- [5. getting k8s events](#5-getting-k8s-events)


# 1. Management tools for clusters, pods, deployments, etc. : 

k9s

# 2. When not able to delete resources in k8s:

First edit resource:

```
kubectl edit <resource name>
```

then delete the `finalizer` part and try again.

# 3. filtering docker images

```shell
docker image "name*"
```

# 4. save and load docker images

```shell
docker image save > smartcity_images
docker image load < smartcity_images
```

# 5. getting k8s events

```
kubectl get events
```
