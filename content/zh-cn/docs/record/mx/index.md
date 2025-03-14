---
title: "MX记录"
linkTitle: "MX记录"
weight: 60
date: 2025-03-12
description: >
  将一个网域的电子邮件定向到托管该网域用户帐号的服务器
---

邮件交换 (MX) 记录将一个网域的电子邮件定向到托管该网域用户帐号的服务器。如果您是 G Suite 用户，要设置 Gmail，则需要将 MX 记录定向到 Google 邮件服务器。一个网域可定义多条 MX 记录，每条记录有不同的优先级。如果邮件通过最高优先级记录无法递送，则采用第二优先级，以此类推。

### RDATA格式

MX 记录的 RDATA 格式如下：

```bash
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                  PREFERENCE                   |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    /                   EXCHANGE                    /
    /                                               /
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

格式说明：

| 值         | 含义                                                         |
| ---------- | ------------------------------------------------------------ |
| PREFERENCE | 16 位整数，它规定在同一所有者内，众多 RR 间，给与这个 RR 的优先权。值越低优先权越高。 |
| EXCHANGE   |     一个`<domain-name>`，它指定愿意为所有者名称充当邮件交换的主机。|

