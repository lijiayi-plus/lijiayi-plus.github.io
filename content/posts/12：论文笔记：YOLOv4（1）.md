---
title: "22：论文笔记：YOLOv4（1）"
date: "2026-05-08T17:15:10+08:00"
slug: "12：论文笔记：YOLOv4（1）"
tags: ["学习记录"]
aliases: ["/2026/05/08/12：论文笔记：YOLOv4（1）/"]
---

# Abstract

这是一篇2020年的paper，代表着yolov4的出现，也是一个小的里程碑maybe。首先在此之前的yolov3，在模型的多尺度预测和深度的网络，有一些提升。小目标检测的性能更加的优良。

有很多的特征能够提高卷积神经网络的性能，这一篇论文似乎是对于这些进行了一个测试
>We assume that such universal features include Weighted-Residual-Connections (WRC), Cross-Stage-Partial-connections (CSP), Cross mini-Batch Normalization (CmBN), Self-adversarial-training (SAT) and Mish-activation.

>We use new features: WRC, CSP, CmBN, SAT, Mish activation, Mosaic data augmentation, CmBN, DropBlock regularization, and CIoU loss, and combine some of them to achieve state-of-the-art results:

WRC、CSP、CmBN、SAT、Mish激活、Mosaic数据增强、CmBN、DropBlock正则化和CIoU损耗，本篇论文使用这些结构的结合实现了sota。

# Results && Conclusions

目前最先进的探测器，速度更快，精度更高。GPU推断时间短，这里面使用帧率生成进行比较，是infra方面的性能的考虑。用的都是老掉牙的GPU架构了。都适合单GPU的运行，想必这回又得是使用2080TI了。

结合第一张图可以看到，在高帧率（快速）的检测场景下，V4具有很高的精确度，属实算是两方面实现兼容了。
# Introductions

过去的很多模型，在速度和准确性上会存在一个矛盾，而这个工作是为了最优化这一些东西。优化并行能力，实现高速的计算。
![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260508164325903.png)
- 这里面的one-stage，和two-stage，就是yolo系列和faster r-cnn中的一个显著的差异，两步的检测精度高，速度慢
- backbone方面，常见有经典的分类网络比如ResNet-50/101，yolo系列的专用骨干网络Darknet53，我都不太知道是啥哈哈。
- neck，特征融合层，FPN：基础特征金字塔，自上而下融合；PANet：在 FPN 基础上加了自下而上的路径增强；Bi-FPN：双向加权特征融合（EfficientDet 用的），也不是很懂捏。

# Related works
## Object detection models

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260508170210082.png)
感觉伟大的论文可以让复杂的论文变得亲近很多。

## Bag of freebies

我们称这些仅改变训练策略或增加训练成本的方法为“免费赠品袋”。数据增强的目的是增加输入图像的变异性，使设计的物体检测模型对不同环境获得的图像具有更高的稳健性。

光度畸变和几何畸变是两种常用的数据增强方法，它们确实有利于物体检测任务。在处理光度畸变时，我们调整图像的亮度、对比度、色调、饱和度和噪声。对于几何畸变，我们增加了随机缩放、裁剪、翻转和旋转。

不仅有基于像素的数据增强，还有基模拟物体遮挡问题的，对于一块一块进行的数据增强，比如说随机的选取和替换某一些部分。

>In dealing with the problem of semantic distribution bias, a very important issue is that there is a problem of data imbalance between different classes, and this problem is often solved by hard negative example mining [72] or online hard example mining [67] in two-stage object detector.

面对数据挖掘上的难题，这里面常常不是交给一级的物体探测器，因为这种探测器属于密集预测架构。一般来说，hard negative example mining [72] or online hard example mining还是会给到faster r-cnn这种的两个阶段的网络。

最后是损失函数方面，这一方面也有着很多很多的讲究。

总而言之，以上都是在数据的处理方式上面下文章，没有触及到最后的骨干网络。

## Bag of specials
对于那些只会略微增加推理成本但能显著提升物体检测准确性的插件模块和后处理方法，我们称之为“Bag of specials”。

# 一个小的总结

这是一个非常完善的方法论性质的综述，讲了怎么去搞CV这种东西，我还是非常喜欢的。还需要去看看。
# 参考文献：

1.[(14 封私信 / 80 条消息) 一文全面梳理YOLO系列｜从YOLOv1到YOLOv13，再到YOLO26 - 知乎](https://zhuanlan.zhihu.com/p/1955758533606880689)
