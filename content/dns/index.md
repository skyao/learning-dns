---
date: 2018-11-21T20:20:00+08:00
title: 基础知识
weight: 100
description : "DNS的基础知识"
---



### 什么是DNS？

DNS 是 Domain Name System 的简称，即域名系统。

DNS 实质上是一个 **域名** 和 **IP** 相互映射的分布式数据库，可以理解未用于整理和识别各个域名的网络电话簿。类比电话簿是将“Acme Pizza”之类的名称转换为要拨打的正确电话号码，而 DNS 将“www.google.com”之类的网络地址转换为托管该网站的计算机的物理 IP 地址，如“74.125.19.147”。

DNS 主要功能是将难于记忆的 IP 地址转换为域名，以方便访问。DNS 是互联网的最重要的服务之一。有了 DNS，我们才可以通过域名方便的访问互联网。



### DNS RFC

#### rfc1034

DOMAIN NAMES - CONCEPTS AND FACILITIES

- https://www.ietf.org/rfc/rfc1034.txt
- https://tools.ietf.org/html/rfc1034

#### rfc1035

DOMAIN NAMES - IMPLEMENTATION AND SPECIFICATION

- https://www.ietf.org/rfc/rfc1035.txt
- https://tools.ietf.org/html/rfc1035

#### ~~rfc2052~~

~~A DNS RR for specifying the location of services (DNS SRV)~~ 已废弃，被RFC2782替代

#### rfc2782

A DNS RR for specifying the location of services (DNS SRV)

- https://tools.ietf.org/rfc/rfc2782.txt
- https://tools.ietf.org/html/rfc2782

#### rfc2929

Domain Name System (DNS) IANA Considerations

- https://tools.ietf.org/rfc/rfc2929.txt
- https://tools.ietf.org/html/rfc2929

#### rfc6335

Internet Assigned Numbers Authority (IANA) Procedures for the Management of the Service Name and Transport Protocol Port Number Registry

- https://tools.ietf.org/rfc/rfc2929.txt
- https://tools.ietf.org/html/rfc2929

### 参考资料

- [DNS 原理入门](http://www.ruanyifeng.com/blog/2016/06/dns.html)
- [DNS 基础知识](https://support.google.com/a/answer/48090?hl=zh-Hans)
- [DNS基础知识](http://blog.51cto.com/lee90/1697333)
- [DNS基础知识](https://www.jianshu.com/p/1cd72ebc61fc)