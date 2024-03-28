---
title: '[转载] Red Hat 推出基于 Rust 的「Nova」驱动程序：Nvidia GPU 的更好 Nouveau'
date: 2024-03-28 17:00:00
author:
  - Ankush Das
  - FOSScope
cover: <封面图片地址>
categories:
  - 转载
  - 新闻
tags:
  - Nouveau
  - Nova
  - Red Hat
  - Nvidia
authorInfo: |
  via: https://news.itsfoss.com/red-hat-nova-driver/

  本文由 [<原作者>](<原作者信息页>) 编写，[开源观察](https://fosscope.com/) 转载发布
---

<!-- 所有在被 `<>` 标记的地方都需要被替换成对应的内容 -->

基于 Rust 的 Nvidia 驱动程序？真是令人振奋的消息！

<!-- more -->

在 NVIDIA 发布开源 GPU 内核模块后，Nouveau 驱动的前景十分光明。

尽管 Nouveau 的进展在 NVIDIA 启用 GSP（GPU 系统处理器）支持后，特别是在 Nouveau 的维护者在去年辞职后有所放缓。

现在，Red Hat 的显示驱动团队似乎带着更有趣的东西回到了正轨：**Nova **—— Nouveau 的现代替代品。Red Hat 的软件工程师 Danilo Krummrich 在一个邮件列表上宣布了这个项目。

那么，什么是 Nova 呢？

## Nova：基于 Rust 的绿队 Nvidia 驱动

![red hat nova](https://news.itsfoss.com/content/images/size/w1304/2024/03/redhat-to-replace-noveau-with-nova-driver.png)

Nova 是一个基于 Rust 的 GSP-only 驱动，旨在准备就绪后成为 Nouveau 的继任者。

当然，Red Hat 考虑寻找继任者的原因之一是因为 Nouveau 的主要维护者辞职了。

Danilo 提到，他们希望通过这个项目开发一个更简化并且现代的驱动：

> 有了 Nova，我们看到与 Nouveau 相比能够显著降低驱动程序复杂性的机会的两个原因。首先，Nouveau 的历史架构，特别是在 nvif/nvkm 方面，相当复杂和僵化，需要进行重大重构才能解决某些问题（例如，VM_BIND 的 VMM / MMU 代码中的锁定层次结构问题目前只能通过权宜之计解决）。其次，对于仅 GSP-only  驱动，无需保持前代代码的兼容性。

此外，Red Hat 似乎一直在其 Linux 产品中不断使用更多的 Rust 代码及其优化。

因此，考虑到 Linux 内核正在逐步添加 Rust 组件，他们希望采用 Rust 构建驱动程序并不令人惊讶。

当然，考虑到这是一个雄心勃勃的项目，它也面临着一些挫折，最大的问题是：

> 选择 Rust 作为编程语言后，首先要面临的问题是对核心内核基础设施（例如设备/驱动程序抽象）缺少C语言绑定抽象层。这有点像“先有鸡还是先有蛋”的问题 —— 我们需要有人将抽象层提交到上游，但同时我们也需要这些抽象层来创建一个驱动程序。因此，我们打算在上游开发 Nova，并从仅使用一些基本 Rust 抽象层的驱动程序框架开始着手。

因此，该项目的方法将通过三个主要分支进行，其中 Nova 存根驱动程序（一个模块）依赖于 PCI 和设备分支。

![nova driver](https://news.itsfoss.com/content/images/2024/03/nova-driver.jpg)

你可以查看托管在 Freedesktop 的内核图形开发部分内的  [仓库](https://gitlab.freedesktop.org/drm/nova?ref=news.itsfoss.com) 。

虽然这听起来很酷，但对于开发者来说，提供一个成熟的基于Rust的驱动程序是一个挑战性的任务。当然，这样的项目将带来内存安全性优势、安全性和性能提升的好处。

然而，这一切何时以及如何发生（在不影响采纳的情况下）仍然是一个决定性因素。

无论如何，我所期望的是 Nvidia GPU 用户能在Linux上获得更好的兼容性，因为我曾因 RTX 3000 系列显卡而遇到过不少显示问题。而且，对于Linux来说，一个现代的 Nvidia 显示驱动程序将会带来不少便利😎

在此之前，Nouveau 驱动将继续存在。即使 Nova 作为继任者出现，对于较老的 Nvidia 显卡而言，Nouveau 驱动也将继续存在。

*你对 Nova 驱动有什么看法？在下面的评论中分享你的想法！*

*Via:*[Phoronix](https://www.phoronix.com/news/Red-Hat-Nova-Rust-Abstractions?ref=news.itsfoss.com)
