---
title: VM Related Notes
date: 2021-06-05 15:01:29
categories: 
- Notes
tags:
- VM
---

#### 1. List all VMs:

```shell
virsh list
```

#### 2. List network setting xml:

```shell
virsh net-dumpxml <network>
```
#### 3. list and revert vm from snapshots:
```shell
virsh snapshot-list 476
virsh snapshot-revert --domain freebsd --snapshotname 5Sep2016_S1 --running
```

<!--more-->
