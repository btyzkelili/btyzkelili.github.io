---
layout:     post
title:      "林轩田-机器学习基石-Lecture16"
subtitle:   ""
date:       2019-07-11 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
## 16. Three Learning Principles

### 16.1 Occam's Razor(剃刀)

![](/img/linxuant-jishi/16-1.png)   

什么样叫做简单？为什么简单是好的？

简单的h: 视觉上看起来很简单，只需要少数的参数

简单的H: 有效的h不多就是简单的

简单的h与简单的H之间有联系

![](/img/linxuant-jishi/16-2.png)   

使用简单的模型能够解释资料，可以说资料是有一定的规律性，如果用很复杂的模型，无法辨别资料到底有没有规律性，因为复杂模型可以分开任何资料，所以用简单模型可以表现一定显著性。

先试线性模型，并且要注意，在使用模型时，要用自己想到的最简单的模型

### 16.2 Sampling Bias

![](/img/linxuant-jishi/16-3.png)   

如果抽样有偏差，那学习也会有偏差，所以训练与测试要在同样的分布下，让训练环境与测试环境尽可能相似，如果测试是用时间上靠后的资料做测试，那么我们在训练的时候要强化时间上后面的数据，选验证集的时候不能随机抽样，而要用时间后面的去做验证集。

![](/img/linxuant-jishi/16-4.png)   

用银行现有的客户有没有刷爆信用卡的数据去训练，来预测新用户要不要给他信用卡，这个场景下，银行给的资料是之前系统决定要给信用卡的客户的数据，我们并不知道没给信用卡的客户会不会刷爆信用卡，用之前方法训练出的模型需要做一些调整，否则在真实情况下一个新用户到来时表现不会很好。

### 16.3 Data Snooping(偷看)

视觉上肉眼偷看

![](/img/linxuant-jishi/16-5.png)   

用统计的方式间接偷看：在回归时如果要进行放缩，如果使用了test部分，影响了放缩过程，也算是偷眼看

![](/img/linxuant-jishi/16-6.png)   

根据别人的paper中用到的方法间接得知资料要选择怎样的模型会表现好，也算是一种偷看，而且在这些资料上表现好在真实情况下也不一定表现好

很难做到完全不偷看，通常折衷的方式是做小心使用验证，进行避免用资料做选择，做决定之前不要看资料，时时刻刻心存怀疑，到底经过多少过程得到结果，到底可能被污染的多严重。

### 16.4 Power of Three

![](/img/linxuant-jishi/16-7.png)   

三个领域

![](/img/linxuant-jishi/16-8.png)   

三个理论限制

![](/img/linxuant-jishi/16-9.png)   

三个模型

![](/img/linxuant-jishi/16-10.png)   

三个有效的工具

![](/img/linxuant-jishi/16-11.png)   

三个学习原则

![](/img/linxuant-jishi/16-12.png)   

三个未来的方向




