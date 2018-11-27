---
date: 2018-11-25T20:20:00+08:00
title: Mesos DNS
weight: 411
menu:
  main:
    parent: "case"
description : "Mesos DNS"
---

### 介绍

用于mesos的基于DNS的服务发现，项目地址：

- [源代码@github](https://mesosphere.github.io/mesos-dns/)
- [项目官网](http://mesosphere.github.io/mesos-dns/)
- [文档](http://mesosphere.github.io/mesos-dns/docs/)

### 设计方案

mesos-dns的方案非常简单直白，架构图如下：

![](images/mesos-dns.png)

基本思路是：

- mesos-dns是一个golang开发的独立应用，是一个单独进程，可以集群部署
- mesos-dns启动后，从mesos master获取服务/任务信息，然后用获取的name和ip地址生成DNS记录
- 修改客户端所在的节点的 `/etc/resolv.conf` 文件，将DNS解析服务器指向 mesos-dns 
- 当客户端运行的应用进行DNS解析时，就会连接上mesos-dns，mesos-dns在自己的DNS记录中查找，如果找到就返回，如果没有找到，则代理给外部的DNS服务器

### 实现细节

> Mesos-DNS periodically queries the Mesos master(s), retrieves the state of all running tasks from all running frameworks, and generates DNS records for these tasks (A and SRV records)