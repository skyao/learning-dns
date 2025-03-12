---
title: "概述"
linkTitle: "概述"
weight: 1
date: 2025-03-12
description: >
  DNS Record 概述
---

DNS 记录，在RFC规范中称为 Resource Recode/资源记录，缩写为RR。

## Resource Recode 定义

### RR格式

RR的定义来自 rfc1035 中 3.2 RR definitions。所有的RR都有如下所示的相同的顶层格式：

```bash
                                    1  1  1  1  1  1
      0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                                               |
    /                                               /
    /                      NAME                     /
    |                                               |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                      TYPE                     |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     CLASS                     |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                      TTL                      |
    |                                               |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                   RDLENGTH                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--|
    /                     RDATA                     /
    /                                               /
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

各个字段的具体格式和描述如下：

| 字段     | 格式和描述                                                   |
| -------- | ------------------------------------------------------------ |
| NAME     | 所有者名称（owner name），例如，这个资源记录匹配的节点的名称 |
| TYPE     | 包含 RR TYPE 代码之一的 2 个八位字节（octets）               |
| CLASS    | 包含 RR CLASS 代码之一的 2 个八位字节（octets）              |
| TTL      | 32位有符号整数，指定在再次咨询信息源之前此资源记录可以被缓存的时间间隔。零值被解释为该 RR 仅能用于正在进行的流程，不应当被缓存。例如，总是将零 TTL 分配给 SOA 记录，以便禁止缓存。零值也可以用于极短暂的数据。 |
| RDLENGTH | 无符号 16 位整数，指定以八位字节计的 RDATA 字段的长度。      |
| RDATA    | 可变长度的八位字节字符串，用来描述资源。这个信息的格式取决于资源记录的 TYPE 和 CLASS 。 |

### TYPE 值域

TYPE 字段用于资源记录。注意，这些类型是 QTYPE 的子集。

| TYPE  | 值   | 含义                                                        | 备注            |
| ----- | ---- | ----------------------------------------------------------- | --------------- |
| A     | 1    | a host address/主机地址                                     |                 |
| NS    | 2    | an authoritative name server/权威名称服务器                 |                 |
| MD    | 3    | a mail destination/邮件目的地                               | 被废弃，使用 MX |
| MF    | 4    | a mail forwarder/邮件转发器                                 | 被废弃，使用 MX |
| CNAME | 5    | the canonical name for an alias/别名的正则名称              |                 |
| SOA   | 6    | a marks the start of a zone of authority/标记权威区域的开始 |                 |
| MB    | 7    | a mailbox domain name/邮箱域名                              | EXPERIMENTAL    |
| MG    | 8    | a mail group member/邮件组成员                              | EXPERIMENTAL    |
| MR    | 9    | a mail rename domain name/邮件重新命名域名                  | EXPERIMENTAL    |
| NULL  | 10   | a null RR                                                   | EXPERIMENTAL    |
| WKS   | 11   | a well known service description/众所周知的服务描述         |                 |
| PTR   | 12   | a domain name pointer/域名指针                              |                 |
| HINFO | 13   | host information/主机信息                                   |                 |
| MINFO | 14   | mailbox or mail list information/邮箱或邮件列表信息         |                 |
| MX    | 15   | mail exchange/邮件交换                                      |                 |
| TXT   | 16   | text strings/文本字符串                                     |                 |
| SRV   | 33   | service and protocol/服务和协议                             | 在rfc2052中引入 |

### QTYPE 值域

QTYPE 字段出现在查询的 question 部分。QTYPE 是 TYPE 的超集，因此所有 TYPE 是合
法的 QTYPE。此外，定义有下述 QTYPE：

| QTYPE | 值   | 含义                                                         | 备注            |
| ----- | ---- | ------------------------------------------------------------ | --------------- |
| AXFR  | 252  | A request for a transfer of an entire zone/请求传送整个区域  |                 |
| MAILB | 253  | A request for mailbox-related records (MB, MG or MR)/请求相关邮箱记录(MB、MG 或 MR) |                 |
| MAILA | 254  | A request for mail agent RRs/请求邮件代理 RR                 | 被废弃，参阅 MX |
| *     | 255  | A request for all records/请求所有记录                       |                 |

### CLASS 值域

CLASS 字段出现在资源记录中。定义有下述 CLASS 助记符和值：

| 助记符 | 值   | 含义                     | 备注                                     |
| ------ | ---- | ------------------------ | ---------------------------------------- |
| IN     | 1    | the Internet/互联网      |                                          |
| CS     | 2    | the CSNET class/CSNET 类 | 被废弃，仅在某些被废弃的 RFCs 中用于举例 |
| CH     | 3    | the CHAOS class/CHAOS 类 |                                          |
| HS     | 4    | Hesiod [Dyer 87]         |                                          |

备注：

- CHAOS 应该是指 Chaosnet 吧？一套早期的网络通信协议，详细见 https://en.wikipedia.org/wiki/Chaosnet
- Hesiod 应该是指 **Hesiod** name service，详细见 https://en.wikipedia.org/wiki/Hesiod_(name_service)

### QCLASS 值域

QCLASS 字段出现在查询的 question 部分。QCLASS 值是 CLASS 值的超集；每一个 CLASS 都是合法的 QCLASS。除了 CLASS 值以外，定义有下述 QCLASS：

| QCLASS | 值   | 含义             | 备注 |
| ------ | ---- | ---------------- | ---- |
| *      | 255  | any class/任何类 |      |

## 标准 Resource Recode

下述 RR 定义预期会在所有类中出现，至少有可能。尤其是，NS、SOA、CNAME 和 PTR 将在所有类中使用，并且在所有类中有相同格式。因为它们的 RDATA 格式是已知的，在这些 RR 的 RDATA 部分中的所有域名可以压缩。

`<domain-name>` 是表示为一系列标签的域名，并终止于零长度的标签。`<character-string>` 是单一长度的八位字节，后面跟有字符的数量。`<character-string>` 被看作是二进制信息，其长度最多可达 256 个字符(包括长度八位字节)。

各个RR的详细格式见后面章节。

## 其他

**显性URL转发记录**： 将域名指向一个`http(s)`协议地址，访问域名时，自动跳转至目标地址。例如：将`www.a .com`显性转发到`www.b.com`后，访问`www.a.com`时，地址栏显示的地址为：`www.b.com`。

**隐性UR转发记录L**： 将域名指向一个`http(s)`协议地址，访问域名时，自动跳转至目标地址，隐性转发会隐藏真实的目标地址。例如：将`www.a .com`显性转发到`www.b.com`后，访问`www.a.com`时，地址栏显示的地址依然是：`www.a.com`。
