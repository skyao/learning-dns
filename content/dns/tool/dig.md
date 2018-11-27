---
date: 2018-11-25T20:20:00+08:00
title: dig
weight: 133
menu:
  main:
    parent: "dns-tool"
description : "dig"
---

**dig**（域信息搜索器）命令是一个用于询问 DNS 域名服务器的灵活的工具。

Dig执行 DNS 查询，显示从已查询名称服务器返回的应答。多数 DNS 管理员使用 **dig** 命令 来诊断 DNS 问题，因为它灵活性好、容易使用、输出清晰。虽然通常情况下 **dig** 与命令行参数配合使用，但它也可以按批处理方式从文件读取查询请求。

```bash
dig [@global-server] [domain] [q-type] [q-class] {q-opt} {global-d-opt} host [@local-server] {local-d-opt} [ host [@local-server] {local-d-opt} [...]]
```

详细参数看 `dig -h`。

### 使用案例

简单查询：

```bash
$ dig skyao.io

; <<>> DiG 9.10.3-P4-Ubuntu <<>> skyao.io
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 61118
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;skyao.io.			IN	A

;; ANSWER SECTION:
skyao.io.		599	IN	A	119.28.182.148

;; Query time: 94 msec
;; SERVER: 10.243.28.52#53(10.243.28.52)
;; WHEN: Tue Nov 27 18:45:28 CST 2018
;; MSG SIZE  rcvd: 53
```

指定要查询的记录类型：

```bash
$ dig skyao.io ns

; <<>> DiG 9.10.3-P4-Ubuntu <<>> skyao.io ns
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 31927
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;skyao.io.			IN	NS

;; ANSWER SECTION:
skyao.io.		19119	IN	NS	f1g1ns2.dnspod.net.
skyao.io.		19119	IN	NS	f1g1ns1.dnspod.net.

;; Query time: 0 msec
;; SERVER: 10.243.28.52#53(10.243.28.52)
;; WHEN: Tue Nov 27 18:46:13 CST 2018
;; MSG SIZE  rcvd: 91
```

dig命令最好用的方式是加上`+trace` 选项，然后就可以看到 dig 程序是如何一步一步解析出域名的IP地址的。从这里可以体验 DNS 的递归查询：

```bash
$ dig skyao.io +trace

; <<>> DiG 9.10.3-P4-Ubuntu <<>> skyao.io +trace
;; global options: +cmd
.			179247	IN	NS	l.root-servers.net.
......
.			179247	IN	NS	k.root-servers.net.
;; Received 239 bytes from 10.243.28.52#53(10.243.28.52) in 0 ms

io.			172800	IN	NS	a0.nic.io.
......
io.			172800	IN	NS	ns-a3.io.
io.			86400	IN	DS	57355 8 1 434E91E206134F5B3B0AC603B26F5E029346ABC9
io.			86400	IN	DS	57355 8 2 95A57C3BAB7849DBCDDF7C72ADA71A88146B141110318CA5BE672057 E865C3E2
io.			86400	IN	DS	64744 8 2 2E7D661097A76EAC145858E4FF8F3DDAE5EAEDFD527725BC6F8A943E 4FE23A29
io.			86400	IN	RRSIG	DS 8 1 86400 20181210050000 20181127040000 2134 . MD7BIr97UWfePzWdROfWCXYYKIss1w7PDNDGlkB9H6AGqVL2yZEXiGL9 bKVJEQ7TSC4oZpDjlB0OmlzZHAvui0dS1fF0ZK3R1kqc7svzmCOZIgS9 Lnvp2h6o9S4g7IywaWBltffxdCrZqjtneF+9W0TAmzGKI3GE81PpLbRQ WWxoTcz/wfUTgMWgdTNnjQE/b1I8Bab0nZdSbcdVmy4dl45zqg7lXKPB wtluM8BS73Ejjk4Ss3tai/u/TQhVwLK+b9ZhXYXUBHcruB4M1AOicaw0 uKF/T5K73IRTG2PNYv2vFNV07LD1hTkK7FdHn4QA2MeWQdYF17fS0PVQ /1MNog==
;; Received 804 bytes from 192.58.128.30#53(j.root-servers.net) in 35 ms

skyao.io.		86400	IN	NS	f1g1ns1.dnspod.net.
skyao.io.		86400	IN	NS	f1g1ns2.dnspod.net.
2iui5t1khct6c5o8i2i67rppatgvegqo.io. 900 IN NSEC3 1 1 1 D399EAAB 2J0BQLE6LOOPHCJAUAVJJVSTG25U7I13 NS SOA RRSIG DNSKEY NSEC3PARAM
2iui5t1khct6c5o8i2i67rppatgvegqo.io. 900 IN RRSIG NSEC3 8 2 900 20181218104621 20181127094621 17116 io. mW9xTV3iv5BBocYpA8o6zYp3pYw7Hk5vMCqaXVL7W2+hXZrOxw27vkoy /PiPauXzoByCFx7mY7uA1iG8NTQH3d1HGo2/Js7naepn9dXjxn+LODPw HBtsm94ad83F2B7M9Sz/6Y+6C+L4fkkS7xsIzFGBREFPE90khutCmqa9 6s4=
2dgrnhfe6c36eout03irkmjqepkqj7ro.io. 900 IN NSEC3 1 1 1 D399EAAB 2DHMP300B8T8G9PKLNU3UG0SSUH0BA2C NS DS RRSIG
2dgrnhfe6c36eout03irkmjqepkqj7ro.io. 900 IN RRSIG NSEC3 8 2 900 20181216151728 20181125141728 17116 io. c6xUgTIcrPtkui/IWwsBXvtdRB2iEVslOWXi3ETybrVTtT8lhkirF1Ax AH+wWl4K6hgOnTy0e+h8Q6CeW5jSAGJMbWRUxWUbTgHJIxpvNupflVZr +4IKo3ZwAPbchfU01cKiEMctpmuYLYgE0+Nt/PZZwkdbANvLrp0FwhuU fuQ=
;; Received 582 bytes from 65.22.161.17#53(b0.nic.io) in 152 ms

skyao.io.		600	IN	A	119.28.182.148
skyao.io.		86400	IN	NS	f1g1ns2.dnspod.net.
skyao.io.		86400	IN	NS	f1g1ns1.dnspod.net.
;; Received 117 bytes from 58.247.212.36#53(f1g1ns1.dnspod.net) in 73 ms
```

可以加一个 `+short` 来简化输出：

```bash
$ dig skyao.io +trace +short
NS e.root-servers.net. from server 10.243.28.52 in 0 ms.
......
NS d.root-servers.net. from server 10.243.28.52 in 0 ms.
A 119.28.182.148 from server 14.215.155.170 in 16 ms.
```

最简洁的方式：

```bash
dig skyao.io  +short
119.28.182.148
```



### 参考资料

- [dig 命令 @ IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_72/com.ibm.aix.cmds2/dig.htm)