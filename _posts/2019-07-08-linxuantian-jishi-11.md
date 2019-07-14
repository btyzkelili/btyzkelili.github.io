---
layout:     post
title:      "林轩田-机器学习基石-Lecture11"
subtitle:   ""
date:       2019-07-08 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
## 11. linear models for classification

### 11.1 Linear Models for Binary Classification 

![](/img/linxuant-jishi/11-1.PNG)    
* linear classification是NP问题，所以我们需要找到一种容易解决他的方法，就是利用linear regression和logistics regression作为其上限来求解。

![](/img/linxuant-jishi/11-2.PNG)   
* 将三种err变换为ys形式
* ys物理意义: y代表正确的，s是打分，所以ys代表correctness score

![](/img/linxuant-jishi/11-3.PNG)   
* 0/1 err图像如蓝线所示，sq r err如红线所示，scaled ce err 如黑线所示(scaled是ce err的log<sub>2</sub>形式，为了让黑线与其他两线相交与一点，方便分析)
* 从图上可以看出，较小的ys下，sqr err和0/1 err 都认为是不太好的情况(err 值大)，而d当ys较大时，0/1 err认为较好的情况sqr认为较差，使得sqr err不能代表0/1,对于scaled ce err，它可以较好的代表0/1 err

![](/img/linxuant-jishi/11-4.PNG)   
* 理论推导如上，也就是说，如果我们把logistic/linear regression做好，就也把linear classification做好了，只不过logistic regression的限制更宽松

![](/img/linxuant-jishi/11-5.PNG)   
* 用logistic/linear regression在资料上学习得到**w**，再得到g(x)=sign(**wx**)
* 如果使用linear regression:optimization最简单，有直接公式，但是限制宽松，可能与0/1err有较大差距
* 如果使用logistic regression:由于它是smooth、convex所以可以用梯度下降，optimization也较为简单，但是也只是一个上限
* 如果使用PLA，只有在linear separable时效果比较好
* 所以建议，logistic regression去找到PLA/pocket/logistic regression的w0；更常用logistic regression而不是pocket(因为每轮的工作差不多，但是optimization更简单)

### 11.2 Stochastic Grad.Descent

![](/img/linxuant-jishi/11-6.PNG)   
* PLA每次只需要找到一个不正确的点进行更新O(1)，而logistic regression需要所有点一起去计算梯度，再找梯度下降的方向O(n)，时间上和pocket一样(pocket是计算所有点找比自己手里好的)

![](/img/linxuant-jishi/11-7.PNG)   
* 我们希望logistic的速度可以和PLA一样快，采取的方法是，每次不计算所有点的梯度，而是只随机抽取一个点来计算，理论依据是只抽取一部分点，也可以基本代表整体的分布，只是我们做的更加极端，只抽取一个点
* 随机梯度下降SGD：优点是简单且耗费低，坏处是不稳定，很难决定什么时候停，一般是相信跑够久就停，经验上yita=0.1

### 11.3 Multiclass via Logistic Regression
![](/img/linxuant-jishi/11-8.PNG)   
* 处理多分类问题，可以训练多个二元分类器，每个分类器针对起皱一个类别判断是或否。
* 缺点是会出现多个分类器抢一个类别，或者没有分类器认为是自己类别的点。

![](/img/linxuant-jishi/11-9.PNG)   
* 可以用更soft的方法，每个分类器是logistic regression，判断是自己类别的概率:
* One-Versus-All(OVA) Decomposition: 对每个类别跑一个logistive regression，跑完后选择这些h个里给出分数最高的。优点是有效，坏处是当数据不平均分布(unbalance)的话，全部预测是错误是可能就会有很高的正确率，会让表现变差。
* 对该办法的延申：multinomial('coupled')logistic regression

### 11.4 Multiclass via Binary Classification
![](/img/linxuant-jishi/11-10.PNG)   
* 每次选两个类别做二元分类，最后根据分类器的投票决定到底是哪个类别

![](/img/linxuant-jishi/11-11.PNG)   
* One-versus-ine(OVO) Decomposition
