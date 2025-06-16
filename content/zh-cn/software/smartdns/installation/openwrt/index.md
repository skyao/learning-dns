---
title: "OpenWrt"
linkTitle: "OpenWrt"
weight: 10
date: 2025-06-16
description: >
  OpenWrt 系统上安装 SmartDNS 
---

软件源路径：

https://downloads.openwrt.org/releases/

参考官方安装文档:

https://pymumu.github.io/smartdns/install/openwrt/

## 通过 istore 安装

在 istore 中搜索 smartdns, 然后安装。

备注: 在 cudy3000 这个路由器上，通过 istore 安装 smartdns 后，无法使用。

smartdns 启动后, 后台报错:

```bash
Mon Jun 16 15:27:35 2025 daemon.info procd: Instance smartdns::smartdns s in a crash loop 6 crashes, 0 seconds since last crash
```

## 通过 opkg 安装

在 cudy3000 上通过 opkg 安装 smartdns 后，可以正常使用。

```bash
opkg update
opkg install luci-app-smartdns
opkg install smartdns
```

```bash
/etc/init.d/dnsmasq stop
/etc/init.d/dnsmasq disable

smartdns -c /etc/smartdns/smartdns.conf

ps | grep smartdns
netstat -tulnp | grep 53
```



