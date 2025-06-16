---
title: "设置"
linkTitle: "设置"
weight: 30
date: 2025-06-16
description: >
  设置公共服务器
---



### 在浏览器中启用 DoH

打开浏览器设置。

在“隐私和安全”部分启用“安全DNS”，并选择DNS提供商。

例如，在Chrome浏览器中，选择 Cloudflare 或 Google 作为加密DNS提供者。



### 使用本地 hosts 文件绕过DNS解析

hosts 文件用于将域名直接映射到IP地址，优先级高于DNS服务器。

文件路径：

- Windows：C:\Windows\System32\drivers\etc\hosts

- Linux/macOS：/etc/hosts

添加域名与IP地址映射，例如：

```bash
142.250.190.14 google.com
127.0.0.1 ads.example.com  # 屏蔽广告
```

保存文件后，刷新DNS缓存：

```bash
ipconfig /flushdns   # Windows
```