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

### DNS的历史

> 备注：以下这小段摘抄自同事的笔记，特此鸣谢

DNS 协议可以追溯到1973年12月发布的 RFC597，当时还没有 Domain Name 的概念，只有 Hostname，早期的 Hostname 使用 "-" 分隔，不区分大小写，由 NIC 在线维护，甚至还有一份打印版需要定期发布。

```bash
   A version of this list will be available online at the
   NIC, the location to be announced with the official Hostname list.
   (Other sites are encouraged to make copies of this list available on
   their own systems.)  In addition, a printed version will be issued
   periodically as part of the Resource Notebook
   Host   Address  Hostname        (Interface)->   Status/
   (8)     (10)                    Computer        System
    -----------------------------------------------------------------
     1     001     UCLA-NMC        Sigma 7         Server till 12/31/73
                                                   SEX
                                   PDP-11/45       User 1/1/74                                                   ANTS
   101      65     UCLA-CCn        IBM 360/91      Server
   201     129     UCLA-CCBS       (PDP-15)->      limited Server
                                   PDP-10
   002     2       SRI-ARC         PDP-10          dedicated Server
                                                   TENEX, NLS
```

随后发布的 RFC606/RFC608 把这份列表的格式定义为一个 ASCII 文本文件，并且使用 FTP 进行维护。

1981 年发表的 RFC811 开始提出了对于 Host/Address 列表的查询协议，支持三种查询命令，是 DNS 查询的雏形。

```bash
HNAME   (find entry with given name) 使用 Host 查找
HADDR   (find entry with given address) 使用 Address 查找
ALL     (return entire host table) 返回整个列表 -_-
```

多年以后，简单的 user@host 模式随着 Internet 的到来逐渐不堪其用，1982 年 8月发布的 RFC819 年提出 Domain name 的概念，"." 被引入用于构造树形结构的名字，host `istf`  进化为 domain `f.isi.arpa`：

```bash
A descision has recently been reached to replace the simple name field, 
"<host>", by a composite name filed, "<domain>"      
The following example illustrates the changes in naming convention:
      ARPANET Convention:   Fred@ISIF
      Internet Convention:  Fred@F.ISI.ARPA
```

域名层次模型构成了一个向下生长的树：

```bash
                         U
                       / | \
                     /   |   \          U -- Naming Universe
                    ^    ^    ^         I -- Intermediate Domain
                    |    |    |         E -- Endpoint Domain
                    I    E    I
                  /   \       |
                 ^     ^      ^
                 |     |      |
                 E     E      I
                            / | \
                           ^  ^  ^
                           |  |  |
                           E  E  E
```

1987 年 10 月提出的 RFC1034/RFC1035，定义了现在我们所知的 DNS 系统，它包括了域名表和查询系统，定义了域名数据库的结构 RR。从这里开始域名不只是做 IP 地址的映射了，泛化了非常多的用途。

### DNS RFC

#### rfc1034

DOMAIN NAMES - CONCEPTS AND FACILITIES

- https://tools.ietf.org/html/rfc1034

#### rfc1035

DOMAIN NAMES - IMPLEMENTATION AND SPECIFICATION

- https://tools.ietf.org/html/rfc1035

#### ~~rfc2052~~

~~A DNS RR for specifying the location of services (DNS SRV)~~ 已废弃，被RFC2782替代

#### rfc2136

Dynamic Updates in the Domain Name System (DNS UPDATE)

- https://tools.ietf.org/html/rfc2136

#### rfc2181

Clarifications to the DNS Specification

- https://tools.ietf.org/html/rfc2181

#### ~~rfc2137~~

~~Secure Domain Name System Dynamic Update~~ 已废弃，被RFC3007替代

#### rfc2782

A DNS RR for specifying the location of services (DNS SRV)

- https://tools.ietf.org/html/rfc2782

#### rfc2929

Domain Name System (DNS) IANA Considerations

- https://tools.ietf.org/html/rfc2929

#### rfc3007

Secure Domain Name System (DNS) Dynamic Update

- https://tools.ietf.org/html/rfc3007

#### rfc6335

Internet Assigned Numbers Authority (IANA) Procedures for the Management of the Service Name and Transport Protocol Port Number Registry

- https://tools.ietf.org/html/rfc2929

#### rfc6763

DNS-Based Service Discovery

- https://tools.ietf.org/html/rfc6763

### 参考资料

- [DNS 原理入门](http://www.ruanyifeng.com/blog/2016/06/dns.html)
- [DNS 基础知识](https://support.google.com/a/answer/48090?hl=zh-Hans)
- [DNS基础知识](http://blog.51cto.com/lee90/1697333)
- [DNS基础知识](https://www.jianshu.com/p/1cd72ebc61fc)