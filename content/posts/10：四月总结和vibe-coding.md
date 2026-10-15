---
title: "20：四月总结和vibe coding"
date: "2026-05-05T21:01:35+08:00"
slug: "10：四月总结和vibe-coding"
cover: "https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/bf0a873999ea9d67cd3d97ff8ea3b753.jpg"
tags: ["学习记录"]
aliases: ["/2026/05/05/10：四月总结和vibe-coding/"]
---

>工具飞速迭代，我想，有一个朴素地辩证法。我们能发挥出的实力，是自己的内涵+工具的外延。如果工具飞速进步，而我们的大脑不断地萎缩，那我们最后是能够担起大任的吗。显然不是。

> 所以，核心在于，让自己变得更聪明，而不是让工具变得更智能。外本内末，歧路亡羊。我还是要去走那一条最为艰难的道路

我想，何其有幸，我的确是接触到了一个，很大程度上的，跨时代的一个工具。事实上，我才接触codex没两天，但目前摆在我面前的，是一个前所未有的，工具，它来自karpathy的一个我认为天才的想法：

*One day, frontier AI research used to be done by meat computers in between eating, sleeping, having other fun, and synchronizing once in a while using sound wave interconnect in the ritual of "group meeting". That era is long gone. Research is now entirely the domain of autonomous swarms of AI agents running across compute cluster megastructures in the skies. The agents claim that we are now in the 10,205th generation of the code base, in any case no one could tell if that's right or wrong as the "code" is now a self-modifying binary that has grown beyond human comprehension. This repo is the story of how it all began. -@karpathy, March 2026*.

是的，现在有没有，到那一天，就是电脑的智能体，真的该去取代人脑的智能体了呢，虽然我才接触codex两天，但我觉得，这是完全可能的。人类是否应该不再需要代码和code，只用去编写md。

这个仓库真的很小很小，小到只有三个核心的文件：prepare.py ,train.py,program.md。一言以蔽之，program不改喂AI，prepare不改，train交给AI比如codex进行一部分的改动。

我问了codex关于这个项目的这样一个问题：

>如果我现在有一个红外小目标检测系统，我能不能通过设置损失函数，输入输出数据，理论结果，而靠模型的迭代推理自动生成全部的模型迭代呢？

它的答案是：

>可以，但不是“只设损失函数就能全自动”。

**结论**

- 你可以把它做成“自动迭代检测模型”的系统，自动化 70%-90% 的实验流程。
- 但“全部自动生成并保证持续创新”不现实，必须先定义好搜索空间和约束。

**要具备的核心要素**

1. 明确目标函数：如 Pd↑、FAR↓、mAP↑、延迟↓、显存↓，合成一个评分函数。
2. 固定评估协议：固定 train/val/test 划分、固定随机种子、固定训练预算。
3. 可搜索模型空间：骨干、检测头、损失项、数据增强、学习率策略的可选集合。
4. 自动闭环：生成候选 -> 训练 -> 验证 -> 记录 -> keep/discard -> 下一轮。
5. 防作弊机制：防过拟合、防数据泄漏、失败回滚、OOM/超时处理。

这似乎并不是非常的难如登天，我觉得，我应该试试




---

# 使用vibe coding的一些所见所闻

今天是4月21日，距离接触到codex，以及过了一个多月。
我确确实实感受到了vibe coding的魅力，也深刻的知道了一个点。
如果还只是像周围同学那样，凡事copy代码扔给AI，还只是在网页端进行操作的话，这样的时代即将被淘汰。人的进步速度，很难比得上AI的进化速度，还是那样脑子发昏地凡事问AI，最后没有提升认知，没有留下能力，其可笑也呼？

我还是试了很多次的，最后体现出的结果大概可以由一句话来表示：

>我认为，AI可以在我们框选的范围内，实现局部的最优化和调优，从而达到正常情况下难以匹敌的准确率，而在更加广泛的0-1的过程中，这仍然是值得商榷的。也就是说，human matters

当然，在现在对于AI的vibe coding有了一些新的了解和理解，可以参考这篇文章：
https://mp.weixin.qq.com/s/vmN5-lrCmMXBgHTZHFDkoQ
我一定不会忘记karpathy，改变我认知的人，也是某种AI思想的引路人。
# 一个句号

今天是五月五日，也是五一劳动节的最后一天。我不想再拖拉了，还是要把过去的一些东西给他结结实实的存个档。曾经我经常写blog的时候，很多东西就想着要写完。要有一个好的beginning，好的ending。实际上我会发现，当我花了很多的时间进行一些修饰的时候，这一篇blog可能是很难完成的。所以今天我在我的blog上面更新了很多的库存，这些有些是之前的一些研究，有的是现在的一些思考，但他们最后都记录着我一段时间的理解与思考，所以我在想，他们有必要存在于我的最后的博客里面，成为我一段生活的见证。

这个四月并不平凡，经历了住院，还有住院时间仍然不得停歇的大唐杯与挑战杯，好像我一直都非常的忙碌，没有时间给自己留下很多的记忆，但我们也知道，那不一定正确。稍微记录一点，还有帮学长画图，里面的mask技巧确实让我非常的受用。
![ab26a1c77e6a4cd4aaa857142277a2af.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/ab26a1c77e6a4cd4aaa857142277a2af.png)


好比我在学习的过程中，经常在累的时候就去刷手机，那到最后演变成为了身心的疲惫，那实际上并不快乐，我所希望的，就是去找到更加高级一些的快乐，并且由此来充盈自己。

我很羡慕三月的自己，因为三月的自己确实做了很多的事情，以及，做了非常非常多的记录，我不知道是不是最后这一些记录成就了我自己，但是我会非常的开心。我想，我必须要开始记录了。

活很多，事很杂，我不想要去单一的进行时间的堆砌。因为成长需要脑力，需要时间与空气。而不是在一个阴暗的角落里面，像泥鳅一样阴暗地爬行。还是要去扭住牛尾巴，发现一件或者两件重要的事情，然后去完成那一两件事就够了，不需要做很多。

你已经很棒了，不需要在给自己的大脑添加很多的负载。
你已经很勤奋，不需要在添加压力，损害大脑未来的潜力。
你需要的只是认知，因为在AI快速发展的现在，任何的工具上的能力都会在一定的时间长度下，被AI所取代。那么，我们的任务，我们的使命，在哪里。

我把这一部分生命的感悟，写作“那些花儿”。

他并不是一次偶然的生命体验，相反来得非常的蹊跷。和父母吃完饭的下午，我在公园里散步。如果我非常的有精力，想必我一定会走很远，拍很多的照片。但这一次我太累了，我直接在小径旁边的长凳子上。我好像睡着了，我是在漫天花语中睡着的。旁边几米并没有花，但是随着风的吹拂我尝到了非常好闻的花香，还有在风的吹拂后，夹带着下了雨后森林的味道，我不知道这种形容是否贴切，又或者是不是我对它后期的美化以及一些依稀的映像，但我知道，这的确是我的生命中的一次非常高潮的生命体验。

想必这样一种触动，他不可言说。他人无法体味，但是却实实在在的，充斥着我的生命乐趣，我想，这很美妙。
![](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/f6b5c0bbf46d77b96a75f7e59240e1ab.jpg)
![bf0a873999ea9d67cd3d97ff8ea3b753.jpg](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/bf0a873999ea9d67cd3d97ff8ea3b753.jpg)
![cf6380b0acf5e640efce90ffda6a78c6.jpg](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/cf6380b0acf5e640efce90ffda6a78c6.jpg)
![1ac142db8c2b30b84b2adc88e5674421.jpg](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/1ac142db8c2b30b84b2adc88e5674421.jpg)

我希望，将那一朵鲜花和他的美丽，融进生命的一个角落。有一些花不需要盛大，但你可以等待它去生根发芽。

>不用躲，些许风霜罢了；
>那股肆意，命运夺不走。



