---
title: "nslookup"
linkTitle: "nslookup"
weight: 20
date: 2025-03-12
description: >
  支持交互模式和非交互模式
---

nslookup支持交互模式和非交互模式。

## 非交互模式

进入非交互模式,即一次性执行一次查询操作就结束,如果直接在nslookup命令后加上所要查询的IP或主机名，那么就进入了非交互模式。当然，也可以在第二个参数位置设置所要连接的域名服务器。

```bash
nslookup [-option] [name | -] [server]
```

可以通过`man nslookup` 查看详细信息。

简单的直接查询：

```bash
$ nslookup skyao.io
Server:		10.243.28.52
Address:	10.243.28.52#53

Non-authoritative answer:
Name:	skyao.io
Address: 119.28.182.148
```

指定要使用的DNS服务器：

```bash
$ nslookup skyao.io 8.8.8.8
Server:		8.8.8.8
Address:	8.8.8.8#53

Non-authoritative answer:
Name:	skyao.io
Address: 119.28.182.148
```

指定记录类型：

```bash
$ nslookup -query=ns skyao.io
Server:		10.243.28.52
Address:	10.243.28.52#53

Non-authoritative answer:
skyao.io	nameserver = f1g1ns2.dnspod.net.
skyao.io	nameserver = f1g1ns1.dnspod.net.

Authoritative answers can be found from:
```

## 交互模式

进入交互模式有如下方法:

1. 直接输入nslookup命令，不加任何参数，则直接进入交互模式，此时nslookup会连接到默认的域名服务器（即/etc/resolv.conf的第一个dns地址）。
2. 是支持选定不同域名服务器的。需要设置第一个参数为“-”，然后第二个参数是设置要连接的域名服务器主机名或IP地址。例如可以设置本机为域名服务器`nslookup - 127.0.0.1`

进入交互模式，然后简单查询：

```bash
$ nslookup
> skyao.io
Server:		10.243.28.52
Address:	10.243.28.52#53

Non-authoritative answer:
Name:	skyao.io
Address: 119.28.182.148
```

通过 set 命令设置查询不同的信息：

```bash
> set type=ns
> skyao.io
Server:		10.243.28.52
Address:	10.243.28.52#53

Non-authoritative answer:
skyao.io	nameserver = f1g1ns2.dnspod.net.
skyao.io	nameserver = f1g1ns1.dnspod.net.

Authoritative answers can be found from:
```

具体的set 参数，或者交互模式下的更多命令，请参考  `man nslookup`。

## 参考资料

- [nslookup 命令@IBM knowledge Center](https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_71/com.ibm.aix.cmds4/nslookup.htm): 不是linux，有细微差别