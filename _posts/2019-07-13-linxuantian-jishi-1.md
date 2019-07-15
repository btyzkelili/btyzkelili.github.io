---
layout:     post
title:      "林轩田-机器学习基石-笔记1"
subtitle:   ""
date:       2019-07-13 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 一. When Can Machines Learn?
---  
## Lecture 1: The Learning Problem
--- 
#### 1.1 What is Machine Learning?  
![](/img/linxuant-jishi/1.jpg)  
* 机器学习处理数据提高某方面的表现  

#### 1.2 Application of Machine Learning?  
![](/img/linxuant-jishi/2.jpg)  
 1. 存在某些可以学习（可以预测）的潜藏模式，某种表现可以增进  
 2. 不知道如何定义 eg.无法定义什么是树 
 3. 模式有data     
* Example:   
![](/img/linxuant-jishi/3.jpg)  
![](/img/linxuant-jishi/4.jpg)  

#### 1.3 Components of Machine Learning  
![](/img/linxuant-jishi/6.jpg)  
1. 输入input：**x**=(x<sub>1</sub>,x<sub>2</sub>,...,x<sub>b</sub>),每个x代表一个特征的值，一个特征可以用多维向量表示  
2. 输出output: y(label)  
3. 目标函数f：未知(需要学习的模式，知道就不用使用机器学习)  
4. 数据(**x**,y)  
5. 假说函数g:尽可能与f相似  

#### 1.4 The Learning Model  
![](/img/linxuant-jishi/5.jpg)  
* 机器学习演算法A:有两个输入：数据和H(hypothsis set),任务是从很多可能的公式h(**x**)组成的H(hypothesis set)中选一个它认为最接近f的g  
* 机器学习模型：A and H
* 机器学习进一步定义：使用数据计算尽可能接近f的g  
* Example:   
![](/img/linxuant-jishi/7.jpg)  
![](/img/linxuant-jishi/8.jpg)  

#### 1.5 Machine and other disciplines  
 ![](/img/linxuant-jishi/11.jpg)  
* 机器学习和数据挖掘在实际中很难区分，但是并不是一样的  
   
![](/img/linxuant-jishi/10.jpg)  
* 机器学习是实现人工智能的一个方法  
  
![](/img/linxuant-jishi/9.jpg)  
* 统计方法有很多机器学习可以借鉴的方法  

## Lecture 2: Learning to Answer Yes/No
--- 
#### 2.1 Perceptron Hypothesis Set
![](/img/linxuant-jishi/2-1.jpg)  
* h=hypothesis=perceptron(感知器)  
* h(x)计算向量x的得分-门槛值  

![](/img/linxuant-jishi/2-2.jpg)  
* x<sub>0</sub> = 1  
* w<sub>0</sub> = -threshold 

![](/img/linxuant-jishi/2-3.jpg)   
* 向量**x**=(x<sub>1</sub>,x<sub>2</sub>)：平面中的点  
* y：称为labels，一个特征向量x对应一个y,对应图中x或者o  
* h：平面中的线，线的一边为positive，另一边为negative 
 
#### 2.2 Perceptron Learning Algorithm(PLA)
![](/img/linxuant-jishi/2-11.jpg)    
* **Perceptron Learning Algorithm(PLA)**  

![](/img/linxuant-jishi/2-4.jpg)   
* 从**w**全为0的线开始，以某种顺序（正序、乱序等）找划分错误的点，根据该点修正**W**（图右侧向量转角方法:夹角为锐角向量乘积为正，直角为0，钝角为负），直到直线满足所有点。  

![](/img/linxuant-jishi/2-5.jpg)     
* **w**所示直线是划分直线h=**w<sup>t</sup>x**的法线,规定了原点之后，原点指向其他点的线即为该点的向量，因为向量之间锐角乘积为正，钝角为负，所以垂直于**w**向量的线是正负分界线，即每当确定一个**w**后，会产生一个分界线h，很多h(**x**)构成H，最终从H中选出最好的h去接近f  

* Example  
![](/img/linxuant-jishi/2-6.jpg)  
	* 不选B原因：y<sub>n</sub>=0(?)  

#### 2.3 Guarantee of PLA
1. PLA一定会停止吗？  
	* necessary condition: Linear Separability(线性可分)
	* 假设线性可分，PLA会停下来（推导过程:02.pdf）
	* 向量内积：![](/img/linxuant-jishi/2-7.jpg)，正则化内积：两个向量内积越大离得越近，内积最大为1
2. 停止了一定正确吗？  

#### 2.4 Non-Separable Data
**Pocket Algorithm**   
![](/img/linxuant-jishi/2-10.jpg)  
线性可分用PLA,如果数据不是线性可分：PLA变形->Pocket，手里握着当前最好的线，比较下一条线是否更好，速度比PLA慢.

* 是非题：线性可分：PLA &ensp;&ensp;&ensp; 非线性可分：Pockest Alorithm

## Lecture 3: Types of Learning
---  
#### 3.1 Learning with Different Output Space y(输出空间)
##### 3.1.1 Binary Classification
##### 3.1.2 Multiclass Classification
##### 3.1.3 Regression(回归)
![](/img/linxuant-jishi/3-2.jpg)  
* 输出是实数(输出空间无限大)
##### 3.1.4 Structured Learning
![](/img/linxuant-jishi/3-1.jpg)  
* 像很大的类别分析，输出空间有某种结构关系

#### 3.2 Learning with Different Data Label y<sub>n<sub>
##### 3.2.1 Suervised
##### 3.2.2 Unsupervised/分群
##### 3.2.3 Semi-supervised
##### 3.2.4 Reinforcement Learning
* 没有最后想要结果的标记，但有一些辅助标记，可以知道动作好坏，用奖励或乘法方式告诉输出好不好。

#### 3.3 Learning with Different Protocol f->(**x**<sub>n</sub>,y<sub>n</sub>)（与机器沟通方式）
##### 3.3.1 Batch Learning
* 一次喂给全部数据，得到一个g
##### 3.3.2 Online Learning
* 每次得到部分数据，每轮的g越变越好
* PLA适用于online protocol
* RL常用online protocol
##### 3.3.3 Active Learning
* 机器有问问题的能力，希望能通过有技巧问问题来用更少的标记学习，常用在取得标记很贵的场合。

#### 3.4 Learning with Different Input Space **x**
##### 3.4.1 Concrete(具体) Features
##### 3.4.2 Raw Features
* image pixels,speech signal,etc
* 需要人或者机器自己去转换成具体的
##### 3.4.3 Abstract Features
* 没有物理意义的输入，eg:用户id
* 需要人或者机器自己去转换成具体的

## Lecture 4: Feasibility of Learning
---
#### 4.1 Learning is impossible?
* no-free-lunch：没有方法证明g在未学习资料上与f到底有多接近，除非加一些假设：
![](/img/linxuant-jishi/4-4.jpg)  
* Hoeffding's Inequslity  
	在N较大的时候，部分抽样的分布可以大概率上表示整体
* PAC:probably approximately correct  
##### 4.1.1 Prove Learning is possible 
![](/img/linxuant-jishi/4-1.jpg)  
![](/img/linxuant-jishi/4-2.jpg)  
* 把一个机器学习问题的所有数据看做瓶子中的弹珠，对于一个确定的h,将h(**x**)=f(**x**)的弹珠看做黄色的，h(**x**)!=f(**x**)看做蓝色的，从瓶子中抽出部分弹珠（训练数据），在选出的珠子和瓶子中的珠子分布相同的前提下，瓶子里面是黄色弹珠的概率可以在很大概率上看作是整个瓶子的黄色珠子概率（PAC）（但有较小可能选出的珠子情况与瓶子内的珠子情况有很大不同），通过此方法以验证一个h的好坏。  
![](/img/linxuant-jishi/4-3.jpg)    
* E<sub>in</sub>(h):在抽出的珠子中h(**x**)!=f(**x**)的概率
* E<sub>out</sub>(h)：在所有珠子中h(**x**)!=f(**x**) 
* 根据上面的分析，可以得到：对确定的f，当E<sub>in</sub>小的时候大概率上E<sub>out</sub>也小，即h很接近f
* 上面只分析了对于一个确定的h得到的结论，但是机器学习是从很多h组成的H中挑选出g，那么学习是可能的吗？
![](/img/linxuant-jishi/4-5.jpg)  
* H由很多h构成，很多h会恶化选出珠子与整个瓶子内珠子情况不同的概率（eg.150个人扔铜板5次，有99%的概率会有人五次都是正面，但对于一个人来说五次都是正面的概率很小），这使得A选出的E<sub>in</sub>小的不一定E<sub>out</sub>也小，那么出现这种情况的可能性有多大呢？下面可以证明在h有限的情况下，这个概率为0.
![](/img/linxuant-jishi/4-6.jpg)  
* 对于一个h，每次抓出一些珠子看做D<sub>n</sub>，BAD表示E<sub>in</sub>和E<sub>out</sub>相差很远，Hoeffding说明在格子中是BAD的比较少，即少数不能代表多数的可能性比较小。
![](/img/linxuant-jishi/4-7.jpg)  
* 对于很多h，只有所有h都可以用少数正确验证多数的D才不会出现上面分析的误选了E<sub>in</sub>小但是实际上E<sub>out</sub>大的情况，这时的D才是好D  
![](/img/linxuant-jishi/4-8.jpg)  
* 只要有一个h上是BAD,整体上就是BAD,计算整体上是BAD的概率如上，其中M=h的数量，exp(..)趋于0，所以当M有限的时候，整体BAD的概率趋于0，即所有h的E<sub>in</sub>都接近于E<sub>out</sub>,此时A可以选E<sub>in</sub>最小的h，而这个h不会是上面提到的恶化坏概率的情况。
##### 4.1.2 summary
* 1.挑出的珠子分布与整体分布相同 2.h的个数有限，满足以上两个条件，学习是可能的。（对于h个数很大的分析，见后面章节）

