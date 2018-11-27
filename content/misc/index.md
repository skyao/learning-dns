---
date: 2018-11-21T20:20:00+08:00
title: 杂项
description : "未经整理的杂项内容"
---



### aws

https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html

### google

https://k8smeetup.github.io/docs/tasks/federation/federation-service-discovery/#验证公共-dns-记录

体现了google玩dns的功力

Federating clusters brings some goodness, such as
​    Ability to define multi-clusters services, replicasets/deployments, ingresses,
​    Failover of services between zones
​    Single point of service definition

### mesos

https://mesosphere.github.io/mesos-dns/ mesos的dns

### nacos

[阿里Nacos发布0.5.0版本，轻松玩转动态DNS服务](https://mp.weixin.qq.com/s/bI7yFS8rNX0yuACmmdUIug)

有人帮写了优点了，不用挠头想了。这个玩法就是dns 返回pod ip的方式，走SRV。

ip+port,还要ipvs兜底。VIPSERVER 一直都是要求 LVS 兜底的。但是兜底也要客户端有重试机制。

NACOS 就是开源的 VIPSERVER。



