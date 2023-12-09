---
title: VM Related Notes
date: 2021-06-05 15:01:29
categories: 
- Notes
tags:
- VM
- en
---

#### 1. List all VMs:

```
virsh list
```

<!--more-->

#### 2. List network setting xml:

```
virsh net-dumpxml <network>
```
#### 3. list and revert vm from snapshots:
```
virsh snapshot-list 476
virsh snapshot-revert --domain freebsd --snapshotname 5Sep2016_S1 --running
```
