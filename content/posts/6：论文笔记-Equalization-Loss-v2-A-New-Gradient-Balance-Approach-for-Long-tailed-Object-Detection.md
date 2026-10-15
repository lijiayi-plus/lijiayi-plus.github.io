---
title: "16：论文笔记 Equalization Loss v2   A New Gradient Balance Approach for Long-tailed Object Detection"
date: "2026-05-05T20:15:48+08:00"
slug: "6：论文笔记-Equalization-Loss-v2-A-New-Gradient-Balance-Approach-for-Long-tailed-Object-Detection"
tags: ["学习记录"]
aliases: ["/2026/05/05/6：论文笔记-Equalization-Loss-v2-A-New-Gradient-Balance-Approach-for-Long-tailed-Object-Detection/"]
---

这是一个 **EQLv2 (Equalization Loss v2)** 目标检测项目，基于MMDetection v2框架开发并进行了深度定制。该项目主要解决长尾分布(long-tail distribution)下的目标检测问题——即数据集中大量类别具有极少的样本，导致模型在这些稀有类别上的表现极差。考虑到ddl马上到来，我们对于代码进行先行的处理。https://github.com/tztztztztz/eqlv2。

这个项目代码目前支持COCO、LVIS、OpenImages等多个长尾分布的主流的数据集。

首先我们对于项目的结构进行分析如下：
```text
mmdetection-eql/
├── configs/               # 配置文件目录（37,200+ tokens，核心）
│   ├── end2end/           # EQL/EQLv2 核心配置文件
│   │   ├── eqlv2_r50_8x2_1x.py    # EQLv2配置
│   │   ├── eql_r50_8x2_1x.py      # EQL配置
│   │   └── mask_rcnn_r50_8x2_1x.py # 基础Mask R-CNN配置
│   ├── lvis/              # LVIS数据集配置
│   ├── openimages/        # OpenImages数据集配置
│   ├── decouple/          # 解耦训练配置（BAGS/CRT/LWS等方法）
│   ├── _base_/            # 基础配置模板
│   └── [30+其他算法目录]   # RetinaNet、Faster R-CNN、Cascade等
├── mmdet/                 # MMDetection核心代码（8,800+ tokens）
│   ├── models/            # 模型定义
│   ├── datasets/          # 数据集处理
│   ├── core/              # 核心组件（anchor、bbox、evaluation等）
│   └── apis/              # 高层API接口
├── tools/                 # 训练/测试脚本
│   ├── dist_train.sh      # 多GPU训练启动脚本
│   ├── dist_test.sh       # 多GPU测试启动脚本
│   ├── slurm_train.sh     # Slurm集群训练脚本
│   ├── slurm_test.sh      # Slurm集群测试脚本
│   ├── print_config.py    # 打印配置文件工具
│   └── parse_openimage_metric.py # OpenImages指标解析
├── demo/                  # 演示脚本
├── tests/                 # 单元测试
├── requirements/          # 依赖管理
└── docker/                # Docker配置
```
这是AI生产的一个目录，我们结合这个目录，展开下一步的工作。

对于训练，我们的函数调用逻辑是：
**调用链路**：`dist_train.sh` → `tools/train.py` → `mmdet/apis/train.py` → 加载模型配置(`mmdet/models/detectors/mask_rcnn.py`) → 设置损失函数(`mmdet/models/roi_heads/bbox_heads/losses.py`中注册的`EQL`/`EQLv2`) → 训练循环

# 读论文

这个文章解决的是一个什么问题呢，就是
>a realistic scenario, we are confronted with a more complex situation that the obtained objects show an extreme imbalance in different categories.

数据集极端不均衡下的不平衡，主要是两个方面：
- 尾类数据量和标注太少，模型不足以学习到
- 模型会倾向于打类的数据，学习到大类的特征

这篇论文提到的SOTA是解耦方法，两阶段检测与建模后微调的方法。

对于之前提供的EQL均衡损耗方法，这是一种端到端的重新加权损失函数
![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260502092110679.png)
对于头类别，比值接近1，这意味着正梯度和负梯度的幅度相近;对于尾部类别，梯度接近0，这意味着正梯度被负梯度所覆盖。而我们可以看到，在梯度比这个衡量的因素里，EQL只是增加了一点点，没有很太大的变化，但是v2却增加了非常非常多。

