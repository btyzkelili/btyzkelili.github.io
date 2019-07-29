---
layout:     post
title:      "Machine Learning"
subtitle:   "Classification"
date:       2019-07-29
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Machine Learning
---  
# Classification:Probabilistic Generative Model
## 1. Clssificatin as Regression?
![](/img/lhy_ml/c-1.png)  
Regression对于model好坏的定义不适用于classification，如右图，存在>>1的点时，regression更倾向于向右偏来减小平方和err  

## 2.Probabilistic Generative Model
![](/img/lhy_ml/c-2.png)  
我们要想知道现有的x(一笔资料)时类别一还是类别二，可以计算P(C1/x)，要计算这个概率，需要通过training data得到P(C1)=C1数据个数/总数据个数、
P(C2)、P(x/C1)、P(x/C2)  
P(x)可以知道任意x产生的概率，所以叫做Generative Model(生成模型)  

怎么计算一个在训练集中没有的x的P(x/C1)呢？P(C1)P(C2)好计算，那P(x/C1)、P(x/C2)如何得到？

![](/img/lhy_ml/c-3.png)  ![](/img/lhy_ml/c-4.png)  
我们假设每一个类别的x的产生来自于一个高斯分布，高斯分布有两个参数∑(也就是σ<sup>2</sup>)和μ，任何一个高斯分布都可以sample出这个类别的training data，
但sample出的概率L(μ,∑)不同，假设每笔资料之间独立分布，L(μ,∑)=f(x1)f(x2)...f(xn)(图中n=79笔该类别资料)，找到使L(μ,∑)最大的μ,∑的高斯分布f的结果作为产生x
的概率

为什么要用高斯分布？
![](/img/lhy_ml/c-10.png)  
可以使用任何符合feature特点的其他分布方式

![](/img/lhy_ml/c-5.png) 
当x有k个feature时，类别n的μ<sup>n</sup>(class n的μ)：k-dim vector，∑<sup>n</sup>：k * k matrices：

![](/img/lhy_ml/c-6.png) 
根据以上方法求得P(x/C1)、P(x/C2)、P(C1)、P(C2)，可以计算P(C1/x)，如果P>0.5则认为是class1

* 模型改进：  
![](/img/lhy_ml/c-7.png) 
![](/img/lhy_ml/c-8.png) 
用上面的方法做的效果可能不是很好，一般的做法是让不同类别共享∑，来减少参数数量，并让L(μ<sup>1</sup>,μ<sup>2</sup>,∑)尽可能大(之前是让每一个类别的L(μ,∑)尽可能大，
现在是让所有类别的L(μ<sup>1</sup>,μ<sup>2</sup>,∑)尽可能大)，修改L后，P(C1/x)=0从曲线变成了直线，为什么会变为直线(linear model)？  
![](/img/lhy_ml/c-11.png)  
![](/img/lhy_ml/c-12.png)  
将P(C1/x)变形，其中z可以化简为上图式子，我们假设∑都相等，可以得到z=**w**<sup>T</sup>x+b，所以P(C1/x)=σ(**w**<sup>T</sup>x+b)，也就是一个linear model，
既然如此，我们可以直接找**w**和b，而不用先找N1、N2、μ<sup>1</sup>、μ<sup>2</sup>、∑再计算**w**、b

## 3. Probabilistic Generative Model 步骤：  
![](/img/lhy_ml/c-9.png) 
1. 找到model:P(c1/x)
2. model好坏的评价函数L(μ<sup>1</sup>,μ<sup>2</sup>,∑)
3. 挑选最好的model(可以求微分解)








