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
    Ability to define multi-clusters services, replicasets/deployments, ingresses,
    Failover of services between zones
    Single point of service definition

### mesos

https://mesosphere.github.io/mesos-dns/ mesos的dns

### nacos

[阿里Nacos发布0.5.0版本，轻松玩转动态DNS服务](https://mp.weixin.qq.com/s?__biz=MzU0MzQ5MDA0Mw==&mid=2247484535&idx=1&sn=3b87b123b365079913e6edff900f159f&chksm=fb0beee3cc7c67f5b1b1703e76bae5b0ccfe501142ea40ae0597a759709b0bc5016a2d90149e&mpshare=1&scene=1&srcid=1121O4r9BeeoWuBTCulPHVxF&pass_ticket=6%2Fc9MheaFU%2FDtdlE1SDG%2BJDOjvMLokEwkYNL2TtL7IwCzzgSP8kPPd0xD4YIit6y#rd)

有人帮写了优点了，不用挠头想了。这个玩法就是dns 返回pod ip的方式，走SRV。

ip+port,还要ipvs兜底。VIPSERVER 一直都是要求 LVS 兜底的。但是兜底也要客户端有重试机制。

NACOS 就是开源的 VIPSERVER。



