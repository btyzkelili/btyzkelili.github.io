---
layout:     post
title:      "林轩田-机器学习基石-Lecture10"
subtitle:   ""
date:       2019-07-08 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
## 10.Logistic Regression
### 10.1 Logistic Regression
![](/img/linxuant-jishi/10-4.png) 
![](/img/linxuant-jishi/10-3.png)  
* logictic regression可以看做是soft的二元分类，他要得到的结果不再是0或1，而是一个0~1的值(概率)

![](/img/linxuant-jishi/10-5.png)  
* 理想情况下，我们希望得到(x,P(+1|x))样子的数据，就可以像之前一样做，但实际情况下我们只有y=0/1的数据(就像我们需要告知病人他得病的概率，但是没有人知道这个概率是多少，我们只能知道他最有到底有没有得病)，这个0/1的数据可以看成是理想情况下数据的有噪声版本。

![](/img/linxuant-jishi/10-6.png)  
* 我们先根据w和x计算s，再通过logistic function将s转换到01之间，就可以得到logistic hypothesis

![](/img/linxuant-jishi/10-1.png)  
* logistic function图像如上，它是一个smooth、monotonic(单调)、sigmoid(s型的)函数

![](/img/linxuant-jishi/10-2.png)  
* 那么我们应该怎样定义logistic regression 的 E<sub>in</sub>呢？

### 10.2 Logistic Regression Error
![](/img/linxuant-jishi/10-7.png)  
* 在f情况下(真实情况下的概率)，产生资料D的概率为上图的左边，如果我们假设h非常接近f，那么h也产生资料D的可能性如上图右边(将f替换成h），如果h非常接近f，那么他们产生资料D的概率也很接近，资料D是由f产生的，所以好的h(接近f的h)产生D的概率会很高，就是说，对于很多病人(x1,x2...)他们真实情况下得病的概率(f)为(p1,p2...)，所以会产生有p(x1)p1p(x2)p(1-2)...可能性产生资料((x1,1),(x2,0)...)...，如果有一个h，在它的是否生病的概率下，产生D的概率非常高，说明h和f很接近

![](/img/linxuant-jishi/10-8.png)
* 要求在h在的可能性最大值，就是求上图中的min(化简过程略，较简单)
* cross-entropy error: err(**w**,**x**,y)=ln(1+exp(-y**w****x))

![](/img/linxuant-jishi/10-9.png)
* 找到E<sub>in</sub>之后，怎么找到w使得E<sub>in</sub>最小？

### 10.3 Gradient of Logistic Regression Error
![](/img/linxuant-jishi/10-10.png)
* E<sub>in</sub>的图像如上图左，对其求梯度(求对**w**的偏微分)，最小的E<sub>in</sub>就是使其梯度为0(神经网络是求解试得梯度为0的w的一种方法)
* 这个梯度就是损失函数？神经网络向着减小它的方向改进，直到收敛

### 10.4 Gradient Descent
![](/img/linxuant-jishi/10-11.png)
![](/img/linxuant-jishi/10-12.png)
* 怎么求使得梯度为0的w？由于难以像线性一样直接得到w，所以可以用不断更新w的方法(像PLA)：梯度下降
* 梯度下降：对w往梯度的反方向走

![](/img/linxuant-jishi/10-13.png)
![](/img/linxuant-jishi/10-14.png)
* 如何确定yita呢？应该在坡度大的地方走的步子大一点，坡度小的地方走的步子小一点，所以yita和||E<sub>in</sub>(w)||成正比
* 新的yita叫做学习率
