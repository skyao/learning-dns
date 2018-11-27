---
date: 2018-11-25T20:20:00+08:00
title: host
weight: 131
menu:
  main:
    parent: "dns-tool"
description : "host"
---

host将主机名解析为IP地址或将IP地址解析为主机名。

## 语法

```bash
host [-aCdlriTwv] [-c class] [-N ndots] [-t type] [-W time] [-R number] [-m flag] hostname [server]
```

host 命令会返回主机的 IP 地址（当指定了 HostName 参数时）和主机名（当指定了 Address 参数时）。根据名称解析服务的配置，host 命令还可能显示与 HostName 参数关联的任何别名。 名称解析服务的示例包含 local、nis 和 bind。

### 命令行选项

注意：不同操作系统下的命令行选项会有所不同，下面是ubuntu 16.04的参数：

| 选项     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| -a       | 相当于使用“-v -t *”                                          |
| -c Class | 指定当它搜索非因特网数据时要查看的类。以下是有效类：IN: 因特网类;CHAOS: Chaos类;HESIOD: MIT Althena Hesiod 类; ANY: 通配符（以上任意一个） |
| -C       | 比较权威名称服务器上的SOA记录                                |
| -d       | 等同 -v                                                      |
| -l       | lists all hosts in a domain, using AXFR                      |
| -i       | IP6.INT reverse lookups                                      |
| -n       | 相当于发布 /usr/bin/hostnew 命令。hostnew 命令将执行绑定解析服务。 |
| -N       | changes the number of dots allowed before root lookup is done |
| -r       | 禁用递归处理。                                               |
| -R       | specifies number of retries for UDP packets                  |
| -s       | a SERVFAIL response should stop query                        |
| -t Type  | 指定要查询的记录类型。                                       |
| -T       | enables TCP/IP mode                                          |
| -v       | 详细方式。                                                   |
| -V       | print version number and exit                                |
| -w       | 永远等待 DNS 服务器的一个回答。                              |
| -W       | specifies how long to wait for a reply                       |
| -4       | use IPv4 query transport only                                |
| -6       | use IPv6 query transport only                                |
| -m       | set memory debugging flag `(trace|record|usage) `                          |

`-t Type` 支持的类型有：

| Type  | 记录类型                                                     |
| ----- | ------------------------------------------------------------ |
| CNAME | 别名的规范名称                                               |
| HINFO | 主机处理器和操作系统类型                                     |
| KEY   | 安全密钥记录                                                 |
| MINFO | 邮箱或邮件列表信息                                           |
| MX    | 邮件交换器                                                   |
| NS    | 指定范围的名称服务器                                         |
| PTR   | 如果查询的是 IP 地址，那么此项为主机名；否则，为指向其他信息的指针 |
| SIG   | 签名记录                                                     |
| SOA   | 域的"授权开始"信息                                           |
| TXT   | 文本信息                                                     |
| UINFO | 用户信息                                                     |
| WKS   | 所支持的众所周知的服务                                       |



### 命令行参数

| 参数     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| Address  | 指定解析主机名时要使用的主机的 IP 地址。Address 参数必须是有效的 IP 地址，以点分十进制格式表示。 |
| HostName | 指定解析 IP 地址时要使用的主机的名称。HostName 参数可以是不平常的主机名，也可以是熟知主机名（例如 nameserver、printserver 或 timeserver，如果这些名称存在）。 |
| Server   | 指定查询要使用的名称服务器。可选，如果没有指定则使用 `resolv.conf` 文件中定义的DNS服务器 |

Address 和 HostName 参数必须二选一，Server 可选。

## 使用案例

最简单的查询，默认只有A和MX记录：

```bash
$ host skyao.io
skyao.io has address 119.28.182.148
```

如果要输出全部信息：

```bash
host -a skyao.io
Trying "skyao.io"
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 34465
;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 10

;; QUESTION SECTION:
;skyao.io.			IN	ANY

;; ANSWER SECTION:
skyao.io.		561	IN	A	119.28.182.148
skyao.io.		22	IN	NS	f1g1ns1.dnspod.net.
skyao.io.		22	IN	NS	f1g1ns2.dnspod.net.
skyao.io.		22	IN	SOA	f1g1ns1.dnspod.net. freednsadmin.dnspod.com. 1515202762 3600 180 1209600 180

;; ADDITIONAL SECTION:
f1g1ns1.dnspod.net.	76593	IN	A	61.151.180.44
......
f1g1ns2.dnspod.net.	79458	IN	A	182.140.167.188

Received 315 bytes from 30.102.12.12#53 in 3988 ms
```

查询SOA权威域名服务器:

```bash
$ host -C skyao.io
Nameserver 121.51.128.164:
	skyao.io has SOA record f1g1ns1.dnspod.net. freednsadmin.dnspod.com. 1515202762 3600 180 1209600 180
Nameserver 14.215.155.170:
	skyao.io has SOA record f1g1ns1.dnspod.net. freednsadmin.dnspod.com. 1515202762 3600 180 1209600 180
......
Nameserver 121.51.1.151:
	skyao.io has SOA record f1g1ns1.dnspod.net. freednsadmin.dnspod.com. 1515202762 3600 180 1209600 180
```



### 参考资料

- [host 命令@IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_72/com.ibm.aix.cmds2/host.htm)：信息很清晰，不过和linux上的host命令，有些细微差异。