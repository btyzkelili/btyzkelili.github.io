---
layout:     post
title:      "林轩田-机器学习技法-笔记1"
subtitle:   ""
date:       2019-07-18 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习技法
---
# Embedding Numerous Features:Kernel Models
---
## Lecture 1: Linear Support Vector Machine
---
#### 1.1 Large-Margin Separating Hyperplane
![](/img/linxuantian-jifa/1-1.JPG)  
这三种分割方式都有相同的VC bound，那么哪一种最好呢？
![](/img/linxuant-jifa/1-1.JPG)  
我们希望选择的是第三种，因为我们的训练数据是有噪声的，他可能要比我们看到的偏差一点，所以能容忍这种偏差的分割直线是最好的，这就要求线到距离他最小点的距离越大越好，也就是margin越大越好，那么怎么求这个距离呢？

#### 1.2 Standard Large-Margin Problem
![](/img/linxuantian-jifa/1-2.JPG)  
![](/img/linxuantian-jifa/1-3.JPG)  
![](/img/linxuantian-jifa/1-4.JPG)  
![](/img/linxuantian-jifa/1-5.JPG)  
根据以上推导，我们得到求margin的最大值就是求：
对于所有n都有y<sub>n</sub>(**w<ub>T</sub>x<sub>n</sub>**+b)>=1时，求min(1/2**w<sup>T</sup>w**)
(注意这里的**w**和**x**是没有第0项的)  
例子：
![](/img/linxuantian-jifa/1-6.JPG)  
* 注意: **x<sub>n</sub>** 是X的第n行，**w<ub>T</sub>** = (w1,w2,...,wn)<sub>T</sub>
#### 1.3 Support Vector Machine
少量的数据我们可以计算出来，那么很多的时候如何计算呢？
![](/img/linxuantian-jifa/1-7.JPG)  
虽然之前讲过梯度下降，但是由于现在有很多限制，下降时有很多地方不能走，难以只用梯度下降。我们发现求解的问题形式很像quadratic programming(二次规划)
![](/img/linxuantian-jifa/1-8.JPG)  
我们可以将问题转换为quadratic programming形式(QP问题)
![](/img/linxuantian-jifa/1-9.JPG)  
如果是非线性的，可以通过特征转化解决
#### 1.4 Reasons behind Large-Margin Hyperplane
之前我们只是说有测量误差时，这样margin大的泛化性更好，现在我们通过理论推导证明为什么large-margin表现好:

![](/img/linxuantian-jifa/1-10.JPG)  
可以看到SVM其实是一种正则化，正则化是希望E<sub>in</sub>越小越好，但是为了防止overfitting，所以对w进行限制，而SVM都是对E<sub>in</sub>
是在限制了E<sub>in</sub>最小时，找到更好的**w**，所以SVM和正则化都是把这两件事考虑进去(一体两面)

另一个解释是VC dimension，vc dimension说的是找的这跟线可以产生多少种o或×的排列组合，现在我只想要margin大的线，也就导致了原本符合条件的
组合现在可能就不再符合条件，也使得vc dimension减小，例如：
![](/img/linxuantian-jifa/1-11.JPG)  
可以看到，vc dimension依赖于资料在什么样的空间里(上图是一个单位圆，如果这个圆更大一点，也许三个点就可以shatter)，想要的margin的大小

![](/img/linxuantian-jifa/1-12.JPG)  
新的控制复杂度的方法，largin-margin,就可以配合复杂的非线性feature transform

