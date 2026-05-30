---
title: 在内地连接 cuhk cse 服务器
description: 放弃 VPN 了
date: 2026-05-30
slug: "connect-cse-server"
categories:
  - 杂项
tags:
  - CUHK
weight: 2 # You can add weight to some posts to override the default sorting (date descending)
---

## 前言

试过单挂 cse openvpn, 同时挂 cse openvpn 和 globalprotect(access.cuhk.edu.hk)，都不能连接到 cse 服务器，然后就没招了，再加上还不懂计网，感觉就是红豆生南国————相思了。

死了一次之后跟 deepseek 进行了大量的对话，总结出了在终端中使用 ssh 从内地连接学校 cse 服务器的办法：

### 利用跳板机

在 shell 中输入下列命令

```shell
ssh -o ServerAliveInterval=30 <cse账号>@gw.cse.cuhk.edu.hk
# `-o ServerAliveInterval=30` 可以使 ssh 每隔 30 秒自动从本地电脑发一个空包给服务器，防止中间网络设备因为空闲而切断连接
```

可以看到出现 `<myHome>` 命令提示符

这是一个 rbash (Restricted BASH, 被大幅受限的 Linux Shell )，在这里不可以使用 cat, nano, > 等命令

### 连接 linux1

为了能使用计算资源，还需要进一步连接 linux1

在 rbash 中，输入一下命令

```shell
ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -o ServerAliveInterval=30 <cse账号>@linux1.cse.cuhk.edu.hk
```

可以看到出现 `<linux1>` 命令提示符，表示进入了 bash 命令行，这样就成功地连接到 cse 服务器了

## 后记

第一次没加 `-o ServerAliveInterval=30`，以为万事大吉了，然后看到了 triple uni 中的那篇 [关于 cse vpn 的帖子](https://tripleuni.com/post/731155) 时，发现自己的 ssh 没过几分钟的时候就断掉了，然后问了 deepseek 才补上的 `-o ServerAliveInterval=30`，这不好笑
