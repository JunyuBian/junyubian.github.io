---
title: VM Related Notes
date: 2021-06-05
draft: false
garden_tags: ["en", "notes", "vm"]
summary: " "
status: "growing"
---

- [1. List all VMs:](#1-list-all-vms)
- [2. List network setting xml:](#2-list-network-setting-xml)
- [3. list and revert vm from snapshots:](#3-list-and-revert-vm-from-snapshots)

# 1. List all VMs:

```shell
virsh list
```

# 2. List network setting xml:

```shell
virsh net-dumpxml <network>
```

# 3. list and revert vm from snapshots:
```shell
virsh snapshot-list 476
virsh snapshot-revert --domain freebsd --snapshotname 5Sep2016_S1 --running
```
