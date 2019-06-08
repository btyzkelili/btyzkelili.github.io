---
layout:     post
title:      "林轩田-机器学习基石-Lecture9"
subtitle:   ""
date:       2019-05-04 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 三. How Can Machines Learn?
## Lecture 9: Linear Regression
---  
### 1. Linear REegression Alforithm
![](/img/linxuant-jishi/9-1.jpg)   
* 与perceptron很像，perceptron=h(x)=sign(w<sup>T</sup>x)  
![](/img/linxuant-jishi/9-2.jpg)    
![](/img/linxuant-jishi/9-5.jpg)    
* 线性回归误差计算-squared error
![](/img/linxuant-jishi/9-3.jpg)    
* h(x)是一个以x为变量的方程，而E<sub>in</sub>(w)变成了一个以w为变量的方程。这样一来，我们就把“在H中寻找能使平均误差最小的方程h”这个问题，转换为“求解一个函数的最小值”的问题。X、y来源于D,是固定不变的，因此E<sub>in</sub>(w)是一个关于w的函数，使得E<sub>in</sub>(w)最小的w，就是我们要寻找的那个最优方程的参数。  
![](/img/linxuant-jishi/9-4.jpg)   
*  E<sub>in</sub>(w)图像如上图，使得E<sub>in</sub>(w)最小的w就是使得每个方向的梯度为0的w，即一阶导数为0，多元求导过程如下：  
	由于：![](/img/linxuant-jishi/9-6.jpg) 并且 ![](/img/linxuant-jishi/9-7.jpg)  
	可以得到：![](/img/linxuant-jishi/9-8.jpg)  
	令上式=0，求得w<sub>LIN</sub>：![](/img/linxuant-jishi/9-9.jpg)  
* 当X<sup>T</sup>X可逆时称为pseudo-inserse矩阵X<sup>+</sup>,大部分情况下X<sup>T</sup>X都是可逆的，因为N>>d+1(?)，不可逆时，用其他方式定义X<sup>+</sup>  
![](/img/linxuant-jishi/9-10.jpg)  
### 2.Is Linear Regression a 'Learning Alforithm'?
* 用以w<sub>LIN</sub>为参数的线性方程对原始数据做预测,可以得到拟合值y^=Xw<sub>LIN</sub>=XX†y。称H=XX†为Hat Matrix，帽子矩阵，因为H为 y带上了帽子，成为y^。  
![](/img/linxuant-jishi/9-11.jpg)  
* 这张图展示的是在N维实数空间R<sup>N</sup>中，注意这里是N=数据笔数， y中包含所有真实值，y^中包含所有预测值，与之前讲的输入空间是d+1维是不一样的(?)。X中包含d+1个column(?)  
* y^=Xw<sub>LIN</sub>是X的一个线性组合,X中每个column对应R<sup>N</sup>下的一个向量，共有d+1个这样的向量，因此y^在这d+1个向量所构成的 span(平面)上。  
* 要在这个平面上找到一个向量y^使得他与真实值y之间的距离&#124y−y^&#124最短。不难发现当y^是y在这个平面上的投影时,即 y−y^⊥span时，&#124y−y^&#124最短。所以之前说过的Hat Matrix H，为y戴上帽子，所做的就是投影这个动作，寻找 span上y的投影。  
* Hy=y^，(I−H)y=y−y^。(I为单位矩阵)
* H:对称性H=H<sup>T</sup>,等幂性H<sup>2</sup>=H,半正定：所有特征值为非负数
* trace：矩阵的迹=该矩阵所有特征值的和
![](/img/linxuant-jishi/9-12.jpg)
* 假设y由f(X)∈span+noise构成的(?)。有y=f(X)+noise之前讲到H作用于某个向量，会得到该向量在span上的投影，而I−H作用于某个向量会得到那条与 span垂直的向量，在这里就是图中的y−y^即(I−H)noise=y−y^。y−y^是真实值与预测值的差，其长度就是就是所有点的平方误差之和。于是就有：  
![](/img/linxuant-jishi/9-13.jpg)   
![](/img/linxuant-jishi/9-14.jpg)  
![](/img/linxuant-jishi/9-15.jpg)  
* Ein和Eout都向σ<sup>2</sup>(noise level)收敛，并且他们之间的差异被2(d+1)N给bound住了,有点像VC bound,不过要比VC bound来的更严格一些(因为这里算出的是平均 Ein和Eout)
* 综上，由于E<sub>out</sub>（w<sub>LIN</sub>）是好的，所以学习发生了
### 3.Linear Classification vs. Linear Regression
* regression的最佳w可以直接计算出来，更容易，那么可以用regression来计算classification吗？  
![](/img/linxuant-jishi/9-16.jpg)    
![](/img/linxuant-jishi/9-17.jpg)  
![](/img/linxuant-jishi/9-18.jpg)    
* 由于err<sub>0/1</sub>总小于err<sub>sqr</sub>，所以regression E<sub>in</sub>(w)可以作为classification E<sub>out</sub>(w)的一个上界，所以可以用regression代替classification,效果可能还可以，可以作为基础款分类。
* 也可以用regression直接得到w作为PLA/pocket的初始w，从一个接近最好结果的w开始算法可能会加快计算过程。