---
title: "介绍"
linkTitle: "介绍"
weight: 10
date: 2025-06-16
description: >
  SmartDNS 介绍
---

## 官方网站

网站:

- https://github.com/pymumu/smartdns

- https://pymumu.github.io/smartdns/

> A local DNS server to obtain the fastest website IP for the best Internet experience, support DoT, DoH, DoQ. 
>
> 一个本地DNS服务器，获取最快的网站IP，获得最佳上网体验，支持DoH，DoT，DoQ。


SmartDNS 是一个运行在本地的 DNS 服务器，提供仪表界面，它接受来自本地客户端的 DNS 查询请求，然后从多个上游 DNS 服务器获取 DNS 查询结果，并将访问速度最快的结果返回给客户端，以此提高网络访问速度。 SmartDNS 同时支持指定特定域名 IP 地址，并高性匹配，可达到过滤广告的效果; 支持DOT(DNS over TLS)、DOH(DNS over HTTPS)和 DOQ(DNS over Quic)，更好的保护隐私。

与 DNSmasq 的 all-servers 不同，SmartDNS 返回的是访问速度最快的解析结果。

## 特性

1. **多虚拟DNS服务器**
   支持多个虚拟DNS服务器，不同虚拟DNS服务器不同的端口，规则，客户端。
2. **多 DNS 上游服务器**
   支持配置多个上游 DNS 服务器，并同时进行查询，即使其中有 DNS 服务器异常，也不会影响查询。
3. **支持每个客户端独立控制**
   支持基于MAC，IP地址控制客户端使用不同查询规则，可实现家长控制等功能。
4. **返回最快 IP 地址**
   支持从域名所属 IP 地址列表中查找到访问速度最快的 IP 地址，并返回给客户端，提高网络访问速度。
5. **支持多种查询协议**
   支持 UDP、TCP、DOT、DOH 和 DoQ 查询及服务，以及非 53 端口查询；支持通过socks5，HTTP代理查询;
6. **特定域名 IP 地址指定**
   支持指定域名的 IP 地址，达到广告过滤效果、避免恶意网站的效果。
7. **域名高性能后缀匹配**
   支持域名后缀匹配模式，简化过滤配置，过滤 20 万条记录时间 < 1ms。
8. **域名分流**
   支持域名分流，不同类型的域名向不同的 DNS 服务器查询，支持iptable和nftable更好的分流；支持测速失败的情况下设置域名结果到对应ipset和nftset集合。
9. **Windows / Linux 多平台支持**
   支持标准 Linux 系统（树莓派）、OpenWrt 系统各种固件和华硕路由器原生固件。同时还支持 WSL（Windows Subsystem for Linux，适用于 Linux 的 Windows 子系统）。
10. **支持 IPv4、IPv6 双栈**
    支持 IPv4 和 IPV 6网络，支持查询 A 和 AAAA 记录，支持双栈 IP 速度优化，并支持完全禁用 IPv6 AAAA 解析。
11. **支持DNS64**
    支持DNS64转换。
12. **高性能、占用资源少**
    多线程异步 IO 模式，cache 缓存查询结果。
13. **主流系统官方支持**
    主流路由系统官方软件源安装smartdns。

## 架构

![Architecture](https://github.com/pymumu/test/releases/download/blob/architecture.png)

1. SmartDNS 接收本地网络设备的DNS 查询请求，如 PC、手机的查询请求；
2. 然后将查询请求发送到多个上游 DNS 服务器，可支持 UDP 标准端口或非标准端口查询，以及 TCP 查询；
3. 上游 DNS 服务器返回域名对应的服务器 IP 地址列表，SmartDNS 则会检测从本地网络访问速度最快的服务器 IP；
4. 最后将访问速度最快的服务器 IP 返回给本地客户端。
