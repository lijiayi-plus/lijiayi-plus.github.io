---
title: "32：Strip-net的基本结构"
date: "2026-09-17T22:26:52+08:00"
slug: "23：Strip-net的基本结构"
tags: ["学习记录"]
aliases: ["/2026/09/17/23：Strip-net的基本结构/"]
---

## Strip R-CNN 论文

原文：Strip R-CNN: Large Strip Convolution for Remote Sensing Object Detection

代码仓库：[YXB-NKU/Strip-R-CNN: [AAAI 2026]"Strip R-CNN: Large Strip Convolution for Remote Sensing Object Detection"](https://github.com/YXB-NKU/Strip-R-CNN)
### 网络解决的核心问题

Strip R-CNN 主要解决的是：遥感图像中的高长宽比目标，也就是细长目标，难以提取完整特征，并且难以进行精确定位。

![1.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/1.png)

可以看出strip R-CNN 方法相比其他方法的mAP更高，尤其是在长宽比大的时候优势更明显。
![3.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/3.png)

比较了LSKNet,PKINet,Strip R-CNN 三种方法的结构说，Strip R-CNN的结构Param最小，但mAP最高，说明了它的结构更优。
### 2.网络整体结构
Strip R-CNN 建立在 **Oriented R-CNN** 框架上:
* 使用 StripNet 替换原 Backbone；
* 使用 Strip Head 替换原 Detection Head。
![4.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/4.png)
 这是StripNet Backbone的结构
![5.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/5.png)
这是Strip head的结构
### 实验结果：
1.说明strip R-CNN  FLOPs 低，mAP 高，以此来说明该方法的优越性。
2.消融实验说明了条带卷积核大小的最佳配置(19,19,19,19)，顺序条带卷积优于并行条带卷积以及StripNet 的通用性。
![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260805130121177.png)