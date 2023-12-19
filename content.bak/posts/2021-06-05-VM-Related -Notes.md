---
title: VM Related Notes
date: 2021-06-05 15:01:29
<<<<<<< HEAD
categories: 
- Notes
tags:
- VM
- en
=======
categories:
- Notes
- En
tags:
- VM
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
---

#### 1. List all VMs:

<<<<<<< HEAD
```shell
=======
``` shell
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
virsh list
```

<!--more-->

#### 2. List network setting xml:

<<<<<<< HEAD
```shell
virsh net-dumpxml <network>
```
#### 3. list and revert vm from snapshots:
```shell
=======
``` shell
virsh net-dumpxml <network>
```
#### 3. list and revert vm from snapshots:

``` shell
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
virsh snapshot-list 476
virsh snapshot-revert --domain freebsd --snapshotname 5Sep2016_S1 --running
```
