---
title: "24：记录一次yolo的可视化"
date: "2026-05-22T11:54:02+08:00"
slug: "14：记录一次yolo的可视化"
tags: ["学习记录"]
aliases: ["/2026/05/22/14：记录一次yolo的可视化/"]
---

今天对于baseline的结果进行了可视化，我们对于置信度大于50%的目标进行了画框，高于之前的25%，用于观测对置信度的一些影响。
总体虽然使用的是OBB，也有一些生成的框确实是旋转的框，但是大部分的还是四四方方的，正的。这个比较奇怪，我们需要改正，大部分定位不到物体具体精细的位置。


![P0004_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0004_pred.png)
以上是004，密集排列的话，置信度是不够的。824 1464，但下面这个是很好的。1490 2137
![P0007_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0007_pred.png)
![P0019_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0019_pred.png)

0019harbor，由于背景固定，感觉还是很可以的。
0047密集小车，1126 2167 最后置信度都很小，由于像素很小。和86形成对比，像素没有那么小还是可以检测出来的
![P0047_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0047_pred.png)
![P0086_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0086_pred.png)
由于车顶与车棚的特征，出现了个误检0179
![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260522113655049.png)

0053，斜着挨着导致置信度受到了影响
![P0053_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0053_pred.png)
小船效果还是不错的
![P0799_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0799_pred.png)

这个不是很懂，军舰不太一样？
![P0259_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0259_pred.png)
超大目标检测不到
![P0261_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0261_pred.png)
0683这个就可以
![P0683_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0683_pred.png)



飞机还是很固定的，由于背景固定，效果都不错
![P0168_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P0168_pred.png)
小目标也是OK的
![P1184_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P1184_pred.png)


1234开始，卫星遥感带云遮挡，小目标，对比度小
![P1234_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P1234_pred.png)
1273
![P1273_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P1273_pred.png)
太小就很难
![P1332_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P1332_pred.png)


大小来看，似乎只能小到这个地步
![P1583_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P1583_pred.png)
黑暗情况下，还是要对比度鲜明，比如说飞机和机场

俯仰的角度下，漏检比较多


![P2135_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P2135_pred.png)
看看会不会有云雾的干扰

![P2330_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P2330_pred.png)

小目标检测不出来

![P2331_pred.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/P2331_pred.png)
