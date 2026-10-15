---
title: "17：harness"
date: "2026-05-24T14:26:20+08:00"
slug: "17：harness"
tags: ["学习记录"]
aliases: ["/2026/05/24/17：harness/"]
---

读了一篇文章，链接如下，遂进行一次记录
https://mp.weixin.qq.com/s/77dyufF3MP8stHPS0BApNw

# 几个概念

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524134529805.png)

## rule

rule是对于AI的软约束

什么意思？就是 AI 理论上应该遵守它，但它并不一定真的每次都遵守。尤其当 Rule 越来越多、需求越来越复杂的时候，模型会出现三种典型情况：

1. 它忘了某条 Rule
2. 它觉得某条 Rule 和这次需求“无关”
3. 它知道这条 Rule，但偷懒没做，还给自己找理由

也就可能是reward hacking的出现

## MCP

给一个定义：MCP（Model Context Protocol）本质上是一种标准方式：把「仓库之外的能力」接进 AI 的工作链路里——既能拉取信息，也能在明确边界内触发外部系统的动作。

如果没有MCP，AI通常被锁在
- 本地代码仓库
- 本地脚本
- 当前对话上下文

所以说能分析。能跑代码，但是不能安全结构化的接入更加外层的工程系统

它们的共性是：需要让 AI 在可控边界里调用系统能力，而不是把凭据和即兴命令散落在对话里。MCP 正是这类能力的连接层：把外部系统以 Tool / 资源的形式暴露给 AI，便于被 Rule、Workflow、Scripts 一起约束。

## SKILL

skill的本质失去告诉AI，有些事情你不要临场发挥，不要每次去重新理解，而是严格按照一套固定的步骤进行。

所以skill能够告诉AI，在某一个具体的节点的时候，AI应该怎么去做，这是很重要的。

## sub agent

多个“分工明确”的AI角色。

以前正常的QA，就是一个人既做产品、又做架构、又做开发、又做 QA，最后质量一定很难收口。

所以我们后来引入了多个 Sub Agent，把不同阶段拆开。每个 Agent 只负责自己那一段，把产出写进文档，然后交给下一个 Agent。

这不是什么新发明，但对于AI来说，这就是一个项目组，这就是一个组内竞争带来的效率最大化。

## Workflow

这里面规定的是一种协作的方式，是一个接力赛的规则

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524135318833.png)
所以 Workflow 的核心不是“有一张图”，而是**让每一次前进、暂停、打回、重跑都有明确依据**。

在我们工程里，这套 Workflow 最后被拆成了三层：
- 一层写给人看，告诉大家这条研发链路整体怎么走
- 一层写给系统看，把阶段和迁移边固定下来
- 一层写给具体角色看，明确每个角色接棒时该读什么、交棒时该写什么

这三层合起来，才构成一个真正能长期维护的 Workflow。

## Scripts

这个对于我来说是完全的新名词

如果说 Rule 只是告诉 AI 应该怎么做，Skill 只是给 AI 标准步骤，那 Scripts 就是在说： 你说你做完了没用，得跑过我这关才算。

**真正成熟的 Harness，最后一定会越来越依赖脚本，而不是越来越依赖提示词。**

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524135529944.png)

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524135637744.png)

## 为什么是harness

是一整套让 AI 在工程里稳定产出正确结果的工程系统。
![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524135722352.png)

## 搭建harness之前，需要做什么

技术上，它的主体是一套典型的 Windows 桌面应用技术栈：以 WPF 为界面基础，以 .NET Framework 为主要运行时，围绕本地工程管理、SVN 协作、配置、状态、更新、日志、多语言等能力不断扩展。也正因为它既有前端交互、又有工程逻辑、又有环境和流程问题，所以它特别适合拿来验证一套 Harness 到底能不能撑住复杂项目。

人做的事情是什么？不是下场补代码，也不是在 AI 后面当“高级打字员”，而是一步一步把 Harness Engineering 搭起来：
- 先把需求和设计说透
- 再补上规则
- 再把固定流程做成 Skill
- 再拆出多 Agent
- 再补上脚本门禁和事后验证
- 再补项目地图、任务看板和流程定义文件
## 设计规格工程

很多人一听到 Harness，就想先写 Rule、先拆 Agent、先上脚本。但如果你一开始连“这个工程到底想怎么开发、最终想交付什么样的东西”都没有说清楚，那后面所有约束都会变成无源之水。

所以我们真正的第一步，不是写 Rule，而是先把一个比较完整的设计规格文档和 AI 反复磨透。

这类文档的意义，不是为了“文档看起来专业”，而是为了在项目一开始就把下面这些问题谈清楚：
- 这个版本到底要解决什么问题
- 哪些问题是核心目标，哪些只是顺手优化
- 改动会影响哪些模块
- 哪些行为必须保持兼容
- 最终什么样才算做完

这一轮你偷懒，后面会用十倍时间还回来。

这些来回不只是在改文档措辞，也是我们和 AI 共同加深对需求本身的理解的过程。有时一开始连自己都不确定想要什么，不妨把 AI 拉进需求讨论里，让它帮着追问、掰开选项——真正的需求常常就是在这样的来回里被挖出来的，而不是第一版就写死在纸上。

最终的SPEC长什么样？它必须清晰的写明你的所有需求，指明必要的边界条件（后面的需求分析agent会帮你补充 剩下的边界条件），必须没有任何不确定的词语，例如：建议，可以，推荐，可选等字样。

## rule

ai会忽略rule，ai会绕过rule
![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524140304061.png)

# 为什么要做skill

如果你认真观察，你会发现工程里有一类事情非常适合做成 Skill：

|          |                |
| -------- | -------------- |
| 执行步骤固定   | 每次都要做          |
| 做错一次就很恶心 | 不值得让 AI 每次重新思考 |

# 走到多agent

单个 Agent 很难在长时间、复杂链路的开发里，同时把需求理解、方案设计、风险判断、编码实现、代码自审、测试验证都做好。

有几种做法：
- 强化单agent，但问题在于，这条路越往后走，越像是在把越来越多的责任塞进一个“大而全”的角色里。 它可以让单个 Agent 变得更谨慎，却很难解决“角色冲突”本身。
- 去中心化协作，就像group聊天和moderate，虽然它足够的灵活，但是长期维护以后他的效果堪称灾难
- 结构化调度

这种模式的典型特征是

| 明确有一个项目经理角色  | 明确每个阶段由谁负责          |
| ------------ | ------------------- |
| 明确每一阶段的输入和输出 | 明确什么时候能往前走，什么时候必须回退 |

它的优点也非常明确：

| 流程清晰         | 可控性强    |
| ------------ | ------- |
| 结果可审计        | 很适合文档沉淀 |
| 更方便长期维护和角色替换 |         |
这些东西不是形式主义，而是为了让后续任何一个人、任何一个 AI，在几天后、几周后、几个月后，都还能看懂：

| 这个任务为什么这么做       | 做到哪一步了       |
| ---------------- | ------------ |
| 哪些风险已经处理         | 哪些问题是在哪一层暴露的 |
| 如果现在要继续维护，应该从哪接上 |              |

可以选择固定角色，固定流程。还是使用一个经理去居中调度。

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524140915929.png)

# 一些必要的改进

- 下游开始自己修改上游文档
- 第二轮问题：PM 太容易越界
- 各个 Agent 的专业性都还不够，这里以代码审查和测试这两个 Agent 举例
- Rule 约束开始不够用了
- Agent 会偷懒，于是又补了基线对比

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524141245102.png)

![d695eaef7c213c9f0d4436f5c08d7977.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/d695eaef7c213c9f0d4436f5c08d7977.png)


Rule 再多，本质上还是自然语言约束。
自然语言约束可以管住很多基础行为，但当需求越来越复杂时，它一定会被忽略、被绕过，或者被“解释性执行”。
所以我们后来又往前走了一步： 把很多能判定的约束，尽量落地成脚本。
也就是
- 编译要过，不是口头说“应该没问题”
- 测试要过，不是口头说“理论上没影响”
- 规则扫描要过，不是口头说“这次特殊
只有脚本通过，才算真正开发完成。


开发前先跑一次，开发后再跑一次，做基线对比。
Harness 不是只靠相信 AI，而是靠不断补机制，让它没有太多偷懒空间。

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524141518899.png)


![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524141555104.png)
AI推进了，但是但系统本身并没有真正感知： **这次产出到底是对还是错。**

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524141709732.png)


![ee4cb7edd674c5fac743b492a120c801.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/ee4cb7edd674c5fac743b492a120c801.png)


![4be5d5268ee3c7024aefde7bed893561.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/4be5d5268ee3c7024aefde7bed893561.png)

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524141812276.png)

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20260524141912043.png)

