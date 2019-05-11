---
layout:     post
title:      "林轩田-机器学习基石-Lecture3"
subtitle:   ""
date:       2019-05-11=
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 一. When Can Machines Learn?
## Lecture 3: Types of Learning
---  
### 1. Learning with Different Output Space y(输出空间)
#### 1.1 Binary Classification
#### 1.2 Multiclass Classification
#### 1.3 Regression(回归)
![](/img/linxuant-jishi/3-2.jpg)  
* 输出是实数(输出空间无限大)
#### 1.4 Structured Learning
![](/img/linxuant-jishi/3-1.jpg)  
* 像很大的类别分析，输出空间有某种结构关系
### 2. Learning with Different Data Label y<sub>n<sub>
#### 2.1 Suervised
#### 2.2 Unsupervised/分群
#### 2.3 Semi-supervised
#### 2.4 Reinforcement Learning
* 没有最后想要结果的标记，但有一些辅助标记，可以知道动作好坏，用奖励或乘法方式告诉输出好不好。
### 3. Learning with Different Protocol f->(**x**<sub>n</sub>,y<sub>n</sub>)（与机器沟通方式）
#### 3.1 Batch Learning
* 一次喂给全部数据，得到一个g
#### 3.2 Online Learning
* 每次得到部分数据，每轮的g越变越好
* PLA适用于online protocol
* RL常用online protocol
#### 3.3 Active Learning
* 机器有问问题的能力，希望能通过有技巧问问题来用更少的标记学习，常用在取得标记很贵的场合。
### 4. Learning with Different Input Space **x**
#### 4.1 Concrete(具体) Features
#### 4.2 Raw Features
* image pixels,speech signal,etc
* 需要人或者机器自己去转换成具体的
#### 4.3 Abstract Features
* 没有物理意义的输入，eg:用户id
* 需要人或者机器自己去转换成具体的