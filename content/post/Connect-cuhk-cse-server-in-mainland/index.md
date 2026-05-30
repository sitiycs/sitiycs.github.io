---
title: 在内地连接 cuhk cse 服务器
description: 放弃 VPN 了
date: 2026-05-31 00:00:00+0000
categories:
  - 杂项
tags:
  - cuhk
weight: 1 # You can add weight to some posts to override the default sorting (date descending)
---

### 前言

试过单挂 cse openvpn, 同时挂 cse openvpn 和 globalprotect(access.cuhk.edu.hk)，都不能连接到 cse 服务器，然后就放弃 VPN 了

下面是在终端中使用 ssh 从内地连接学校 cse 服务器的办法

### 利用跳板机

在 shell 中输入下列命令( linux bash 和 windows powershell 均可，mac 不清楚，可以试试)

```shell
ssh <cse账号>@gw.cse.cuhk.edu.hk
```

可以看到出现 <myHome> 命令提示符
这是一个 rbash (Restricted BASH, 被大幅受限的 Linux Shell )，在这里不可以使用 cat, nano, > 等命令

### 连接 linux1

为了能使用计算资源，还需要进一步连接 linux1
在 rbash 中，输入一下命令

```shell
ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null <cse账号>@linux1.cse.cuhk.edu.hk
```

可以看到出现 <linux1> 命令提示符，表示进入了 bash 命令行，这样就成功地连接到 cse 服务器了
