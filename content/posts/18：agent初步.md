---
title: "28：agent初步"
date: "2026-05-24T21:02:42+08:00"
slug: "18：agent初步"
tags: ["学习记录"]
aliases: ["/2026/05/24/18：agent初步/"]
---

# 我给十个codex打工

我还是想用这样的一个题目，参考的是
[(14 封私信 / 80 条消息) 如何有效地给 10 个 Claude Code 打工 - 知乎](https://zhuanlan.zhihu.com/p/2007147036185744607)
我们生在一个巨变的时代，得之则生，弗得则怠。
刚好，前一阵子在刷稀土掘金的时候，刷到了这样一个帖子
https://juejin.cn/post/7611070995847528482?share_token=7ff06389-fa16-4c04-96e6-b925e1919b17
在这里面增加了多agent组队写作的功能，多 Agent 组队协作的功能，不明觉厉，我决定试试。

## 基础要求

首先你得要有一个codex，其次需要有一个ubuntu 22以上的linux环境，对应到autodl的平台上，需要3090/4090就可以了。可以参考我之前的blog内容：5：记录一次autodl的codex配置。

原来的命令需要从github上面拉文件，所以我们可以用autodl的一些小小的优化之学术科研的配置加速
```bash
# 开启autodl学术加速
source /etc/network_turbo
# 2) 指定版本（1.0.5 有 Linux x86_64 资产）并执行安装 
CODEX_REPO=stellarlinkco/codex \ 
CODEX_BASE_URL=https://github.com/stellarlinkco/codex/releases/download/rust-v1.0.5 \ 
bash <(curl -fsSL https://raw.githubusercontent.com/stellarlinkco/codex/main/scripts/install.sh)
```


实际上以上的内容，来自于一个月前，但是现在的思想已经有了很大的变化。

我需要的是什么。

是不是一个远程的手机能够操控ssh的连接，能够让我在手机上面实现vibe coding，这当然很吸引人，毫无疑问的。但是，这对我而言真的必要吗。

如果有一个工作流，需要我时时刻刻去修改，去迭代，我想这只能说明一个问题，这个模型不够健康，这个工作流不够健康。

AI已经完全的超越人类，但是我们却还在用我们弱智的一些理念，和一些可以说是碎片化的想法，去控制着AI的使用。想必这是不太合适的，我们不需要有那么多的控制和interrupt，AI 可以自己完成一个宏大的工作，我们需要给予的，是一个工作流，是一个可以高效完成任务的一个工作流，仅此而已。

所以，我们要去相信，AI完全可以替代人类，也要去相信，人类因为自己的哲学而能够存在于这个世界上。所以，我们不需要的是，让claude code去连接我们的大脑，去压榨我们的生产力，我们应该做的，是让他能够自己工作，合理的工作。

所以，我需要学习agent

# 学习agent

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524204154454.png)
今天我要完成的，就是这样一个任务

## 区分 chatbot、workflow、agent、multi-agent

- chatbot指的是一个聊天机器人，就像deepseek网页版
- workflow是一个工作流，基于确定的流程完成任务
- agent是可以独立完成一个任务的个体，可以自主决定调用工具
- multi-agent是多个agent，以不同的分工来完成一个任务

## 理解 agent 的基本循环：observe -> think -> act -> observe

从接受一个命令，到思考如何去完成，到执行，最后观察完成的结果，决定下一步的动态

## 明白什么时候不该用 agent：

任务可预测、流程稳定、普通脚本能解决时，agent 反而增加不确定性。
这是表达给出的一个点，但实际上。

核心的长治久安，最后都要有一个合适的script

## 读两篇文章

[Building Effective AI Agents \ Anthropic](https://www.anthropic.com/engineering/building-effective-agents)
[A practical guide to building agents | OpenAI](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)

实际上我也没有很清楚，我的科研，是需要一个agent，还是workflow