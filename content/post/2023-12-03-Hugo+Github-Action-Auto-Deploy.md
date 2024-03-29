---
layout: post
title: Hugo Site Auto Deployment with Github Action
subtitle: Hugo Site Auto Deployment with Github Action
description: Hugo Site Auto Deployment with Github Action
excerpt: Hugo Site Auto Deployment with Github Action
date: 2023-12-02
author: Junyu
tags:
    - hugo
    - git
    - notes
URL: "/2023/12/02/Hugo+Github-Action-Auto-Deploy/"
categories: [ Tech ]
---

- [1-Background](#1-background)
- [2-Steps](#2-steps)
- [3-Good to know](#3-good-to-know)
- [Reference](#reference)

# 1-Background

Trying to auto deploy Hugo blogs with Github Action. 

# 2-Steps

Most steps and tips have been covered by reference#1 and reference#2.

# 3-Good to know

Action will build from base url, could use this feature to create different sub domain under github.io. e.g. create a repo called `projects` to display different projects, this will be added to github.io/prjects

If site deployment is automatically triggered by Github Action, need to notice the time difference between Github server and local time zone.

# Reference

1-https://gohugo.io/hosting-and-deployment/hosting-on-github/

2-https://lucumt.info/post/hugo/using-github-action-to-auto-build-deploy/