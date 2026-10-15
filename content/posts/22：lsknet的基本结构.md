---
title: "22：lsknet的基本结构"
date: "2026-09-17T22:26:37+08:00"
slug: "22：lsknet的基本结构"
tags: ["学习记录"]
aliases: ["/2026/09/17/22：lsknet的基本结构/"]
---

  

原文：《LSKNet: A Foundation Lightweight Backbone for  Remote Sensing》

仓库：[zcablii/LSKNet: (IJCV2024 & ICCV2023) LSKNet: A Foundation Lightweight Backbone for Remote Sensing](https://github.com/zcablii/LSKNet)

这个网络解决的核心的问题：是现有的网络，往往只是去看那个目标本身。但是，那失去了很多上下文的信息。LSKnet采用大卷积核的方式，能够获得更大的感受野。同时，LSKnet可以动态调整其感受野，使得其在识别目标及其背景信息中，有很好的检测效果。原文的论述如下：

>In particular, most objects in aerial images may be small and difficult to identify based on their appearance alone. Instead, recognizing these objects relies on their context, as the surrounding environment can provide valuable clues about their shape, orientation, and other characteristics.

其次是一个现实情况：有一些目标需要的上下文信息很少，比如说足球场；有一些目标需要的上下文很大，比如说FSC这种。

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260730081244183.png)

从其主图不难发现，这个网络有两个不同规模的感受野。

## Backbone：LSKNet

### LSKNet-T
- 四阶段通道数：`[32, 64, 160, 256]`
- 四阶段 Block 数：`[3, 3, 5, 2]`
- 主干参数量：约 **4.3M**
### LSKNet-S
- 四阶段通道数：`[64, 128, 320, 512]`
- 四阶段 Block 数：`[2, 2, 4, 2]`
- 主干参数量：约 **14.4M**
## Neck：FPN
最最基础的FPN，并没有使用 PANet、PAFPN、BiFPN 等改进型 Neck
## 检测头：Oriented R-CNN
也是最基础的