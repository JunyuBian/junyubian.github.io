---
title: FD.io简介
date: 2021-04-26
lastmod: 2021-04-26
---

- [关于datapath的创新](#关于datapath的创新)
  - [FD.io解决的问题](#fdio解决的问题)
  - [现有dataplane的缺陷](#现有dataplane的缺陷)
  - [FD.io的简单介绍](#fdio的简单介绍)
    - [与DPDK的关系](#与dpdk的关系)
    - [关于VPP](#关于vpp)


总结自[fd.io Youtube](https://www.youtube.com/watch?v=rfat_guzoEI)

# 关于datapath的创新

> "Innovating the sh.. out of the datapath"

## FD.io解决的问题

就目前来看，相比controlplane，dataplane得到的发展更受局限，我们少有具有推动性的或特性丰富的dataplane，从而导致了数据中心相关创新的缺乏。我们亟需一个灵活的高性能可编程dataplane，所以fd.io，或者说VPP，出现了。

## 现有dataplane的缺陷

当然，现在已经有一些人在做相关dataplane的尝试，但是这些产品总是存在一些不足的点，比如在可扩展性和稳定性方面的不足、缺少跨平台的能力等。这些能力都是很重要的点，比如对于跨平台来说，我们希望dataplane可以在VM上运行，同时也能够通过容器运行。

## FD.io的简单介绍

### 与DPDK的关系

对于IO来说，**主要依赖于DPDK**的实现，可以理解为在DPDK上层**叠加包处理和管理的能力**，从而达到把DPDK集成到多种环境（比如SDN）中的目的。

### 关于VPP

VPP全称是Vector Packet Processor，最初是在Cisco内部于2002年开始创立，一共有300,000行左右代码，现在捐赠给了FD.io。可用于L3网络（IPv4/IPv6）、MPLS、SR和L2网络，是一个高度可编程的多功能数据平面。高度可编程和多功能主要体现在VPP允许**以插件的方式进行集成**，每个插件可以视为一个小的子项目，多个插件的开发增强了VPP的能力，这也使得VPP甚至可以被用于代替vSwitch、vRouter、vFirewall等。

![VPP_Stack.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5e1b621683f64a47b8c6b7df79b2dcd0~tplv-k3u1fbpfcp-watermark.image)

VPP的能力表现是比较稳定的，和包大小、FIB大小、路由数量无关，对比来看OVSDPDK收FIB大小影响极大。