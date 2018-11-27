---
date: 2018-11-25T20:20:00+08:00
title: PTR记录
weight: 127
menu:
  main:
    parent: "dns-record"
description : "PTR记录"
---

PTR记录是A记录的逆向记录，又称做IP反查记录或指针记录，负责将IP反向解析为域名

### RDATA格式

PTR 记录的 RDATA 格式如下：

```bash
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
/                     PTRDNAME                  /
/                                               /
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

格式说明：

| 值       | 含义                                         |
| -------- | -------------------------------------------- |
| PTRDNAME | 指向域名名字空间中某个位置的 `<domain-name>` |
