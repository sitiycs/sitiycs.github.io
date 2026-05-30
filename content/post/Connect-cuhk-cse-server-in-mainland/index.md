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

### 利用跳板机

在 shell 中输入下列命令

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
