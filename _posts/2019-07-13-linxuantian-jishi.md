---
layout:     post
title:      "林轩田-机器学习基石-笔记"
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
### 1.1 What is Machine Learning?  
![](/img/linxuant-jishi/1.jpg)  
* 机器学习处理数据提高某方面的表现  

### 1.2 Application of Machine Learning?  
![](/img/linxuant-jishi/2.jpg)  
 1. 存在某些可以学习（可以预测）的潜藏模式，某种表现可以增进  
 2. 不知道如何定义 eg.无法定义什么是树 
 3. 模式有data     
* Example:   
![](/img/linxuant-jishi/3.jpg)  
![](/img/linxuant-jishi/4.jpg)  

### 1.3 Components of Machine Learning  
![](/img/linxuant-jishi/6.jpg)  
1. 输入input：**x**=(x<sub>1</sub>,x<sub>2</sub>,...,x<sub>b</sub>),每个x代表一个特征的值，一个特征可以用多维向量表示  
2. 输出output: y(label)  
3. 目标函数f：未知(需要学习的模式，知道就不用使用机器学习)  
4. 数据(**x**,y)  
5. 假说函数g:尽可能与f相似  

### 1.4 The Learning Model  
![](/img/linxuant-jishi/5.jpg)  
* 机器学习演算法A:有两个输入：数据和H(hypothsis set),任务是从很多可能的公式h(**x**)组成的H(hypothesis set)中选一个它认为最接近f的g  
* 机器学习模型：A and H
* 机器学习进一步定义：使用数据计算尽可能接近f的g  
* Example:   
![](/img/linxuant-jishi/7.jpg)  
![](/img/linxuant-jishi/8.jpg)  

### 1.5 Machine and other disciplines  
 ![](/img/linxuant-jishi/11.jpg)  
* 机器学习和数据挖掘在实际中很难区分，但是并不是一样的  
   
![](/img/linxuant-jishi/10.jpg)  
* 机器学习是实现人工智能的一个方法  
  
![](/img/linxuant-jishi/9.jpg)  
* 统计方法有很多机器学习可以借鉴的方法  

## Lecture 2: Learning to Answer Yes/No
--- 
### 2.1 Perceptron Hypothesis Set
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
 
### 2.2 Perceptron Learning Algorithm(PLA)
![](/img/linxuant-jishi/2-11.jpg)    
* **Perceptron Learning Algorithm(PLA)**  
![](/img/linxuant-jishi/2-4.jpg)   
* 从**w**全为0的线开始，以某种顺序（正序、乱序等）找划分错误的点，根据该点修正**W**（图右侧向量转角方法:夹角为锐角向量乘积为正，直角为0，钝角为负），直到直线满足所有点。
![](/img/linxuant-jishi/2-5.jpg)   
* **w**所示直线是划分直线h=**w<sup>t</sup>x**的法线,规定了原点之后，原点指向其他点的线即为该点的向量，因为向量之间锐角乘积为正，钝角为负，所以垂直于**w**向量的线是正负分界线，即每当确定一个**w**后，会产生一个分界线h，很多h(**x**)构成H，最终从H中选出最好的h去接近f  
* Example
[](/img/linxuant-jishi/2-6.jpg)  
	* 不选B原因：y<sub>n</sub>=0(?)  

### 2.3 Guarantee of PLA
1. PLA一定会停止吗？  
	* necessary condition: Linear Separability(线性可分)
	* 假设线性可分，PLA会停下来（推导过程:02.pdf）
	* 向量内积：![](/img/linxuant-jishi/2-7.jpg)，正则化内积：两个向量内积越大离得越近，内积最大为1
2. 停止了一定正确吗？  

### 2.4 Non-Separable Data
**Pocket Algorithm**   
![](/img/linxuant-jishi/2-10.jpg)  
线性可分用PLA,如果数据不是线性可分：PLA变形->Pocket，手里握着当前最好的线，比较下一条线是否更好，速度比PLA慢.

* 是非题：线性可分：PLA &ensp;&ensp;&ensp; 非线性可分：Pockest Alorithm

## Lecture 3: Types of Learning
---  
### 3.1 Learning with Different Output Space y(输出空间)

![](/img/linxuant-jishi/3-2.jpg)  
* 输出是实数(输出空间无限大)

![](/img/linxuant-jishi/3-1.jpg)  
* 像很大的类别分析，输出空间有某种结构关系
### 3.2 Learning with Different Data Label y<sub>n<sub>
* 没有最后想要结果的标记，但有一些辅助标记，可以知道动作好坏，用奖励或乘法方式告诉输出好不好。
### 3.3 Learning with Different Protocol f->(**x**<sub>n</sub>,y<sub>n</sub>)（与机器沟通方式）
#### 3.3.1 Batch Learning
* 一次喂给全部数据，得到一个g
#### 3.3.2 Online Learning
* 每次得到部分数据，每轮的g越变越好
* PLA适用于online protocol
* RL常用online protocol
#### 3.3.3 Active Learning
* 机器有问问题的能力，希望能通过有技巧问问题来用更少的标记学习，常用在取得标记很贵的场合。
### 3.4 Learning with Different Input Space **x**
#### 3.4.1 Concrete(具体) Features
#### 3.4.2 Raw Features
* image pixels,speech signal,etc
* 需要人或者机器自己去转换成具体的
#### 3.4.3 Abstract Features
* 没有物理意义的输入，eg:用户id
* 需要人或者机器自己去转换成具体的

## Lecture 4: Feasibility of Learning
---
### 4.1 Learning is impossible?
* no-free-lunch：没有方法证明g在未学习资料上与f到底有多接近，除非加一些假设：
![](/img/linxuant-jishi/4-4.jpg)  
* Hoeffding's Inequslity  
	在N较大的时候，部分抽样的分布可以大概率上表示整体
* PAC:probably approximately correct  
#### 4.1.1 Prove Learning is possible 
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
#### 4.1.2 summary
* 1.挑出的珠子分布与整体分布相同 2.h的个数有限，满足以上两个条件，学习是可能的。（对于h个数很大的分析，见后面章节）

# 二. Why Can Machines Learn?
---
## Lecture 5: Training versus Testing
---
### 5.1 What's learning
![](/img/linxuant-jishi/5-1.jpg)  
* 把learning拆成两部分：  
	1. sure E<sub>in</sub> close to E<sub>out</sub>?  
	2. E<sub>in</sub> small enough?  
* 当M小的时候，坏事发生的概率小，满足条件1，但是可选的h少，不一定能找出足够小的E<sub>in</sub>，不满足条件2；当M大的时候，坏事发生的概率大，不满足条件1，但是可选的h多，可找出足够小的E<sub>in</sub>，满足条件2，由此得知M的重要性
* Example
![](/img/linxuant-jishi/5-2.jpg)  
### 5.2 M
![](/img/linxuant-jishi/5-3.jpg)  
* M:不同h的个数
### 5.3 Growth Function
![](/img/linxuant-jishi/5-4.jpg)  
* 在二维平面所有点上的划分h(直线)个数有无数个，从所有点中选出N个dichotomies(二分):H(**x**<sub>1</sub>,**x**<sub>2</sub>,...,**x**<sub>N</sub>)，在这N个点上的h最多有2<sup>N</sup>个(因为每个点不是o就是x两种情况)
![](/img/linxuant-jishi/5-5.jpg)  
* 将dichotomies:H(**x**<sub>1</sub>,**x**<sub>2</sub>,...,**x**<sub>N</sub>)的最大值看做m<sub>H</sub>(N):成长函数
### 5.4 M Replaced by Growth Function
#### 5.4.1 What if m<sub>H</sub>(N) replaces M?
![](/img/linxuant-jishi/5-6.jpg)  
* 不同情况下的m<sub>H</sub>(N)：  
![](/img/linxuant-jishi/5-7.jpg)    
* 当m<sub>H</sub>(N)是polynomial（多项式）时，不等式右边在N足够大时趋于0，当m<sub>H</sub>(N)是exponential（指数函数）时，不等式右边不趋于0
#### 5.4.2 Break Point of H
![](/img/linxuant-jishi/5-8.jpg)    
* break point:第一个m<sub>H</sub>(k)<2<sup>k</sup>的点k
几种情况下的break point:
![](/img/linxuant-jishi/5-8.jpg)    
* 如果没有break point:m<sub>H</sub>(N)=2<sup>N</sup>
* 如果有break point k:m<sub>H</sub>(N)=O(N<sup>k-1</sup>)(下一节证明)

## Lecture 6: Theory of Generalization
---
### 6.1 Restriction of Break Point
* grow function:m<sub>H</sub>(N) N个点上最多可以产生多少种满足H的点的划分方式(dichotomies点的ox组合)  
* break point=k:当N=k时，成长函数第一次!=2<sup>k</sup>,意味着在有n>=k个点时，这些点中任意k个都不能shatter(shatter:k个点有2<sup>k</sup>种所有的ox组合)  
![](/img/linxuant-jishi/6-1.jpg)  
* 对于上图：k=2，说明在点的个数N=2时，这2个点不可以组合出2<sup>2</sup>种所有ox情况，因为存在某些情况不能满足H（break point定义），同理，当N>2时，不会出现任意2个点它们的组合为2<sup>2</sup>种所有的排序情况，所以当N=3时，最多有5种划分这3个点的方式，即5 dichotomies。

### 6.2 Bounding Function
![](/img/linxuant-jishi/6-2.jpg)  
* bounding funtion B(N,k):在N个点上任意k个点no shatter所能得到的满足H的最多划分方式  
![](/img/linxuant-jishi/6-4.jpg)  
* 当k=1,因为只要超过一划分方式就会有某个点的ox值与第一种划分不同，此时该点shatter，不满足k=1条件，所以B(N,1)=1  
* 当k>N，因为k个点no shtter，而N<k，所以这N个点可以shatter，所以最多有2<sup>N</sup>种点的组合方式。  
* 当k=N，因为不能有N个点shatter，所以最多有2<sup>N</sup>-1种点的组合方式。  
* 其他，![](/img/linxuant-jishi/6-5.jpg)，证明略   

由此得到B(N,k)的上限是有关N的多项式：  
![](/img/linxuant-jishi/6-6.jpg)  
* 当k确定时，B(N,k)被上限多形式poly(N)限制，所以：如果break point存在，成长函数是多项式级。   

### 6.3 Vapnik-Chervonenkis(VC)bound
![](/img/linxuant-jishi/6-7.jpg)  
* 前一章提到的M可以被成长函数替代，并且经过三步证明（略）后可以得到VC bound，证明了E<sub>in</sub>和E<sub>out</sub>相差很大的概率，在成长函数有break point、N足够大时时，趋于0.  
* 到此，证明了H中有无限h时，若成长函数存在break point，那么learning也是成立的  
![](/img/linxuant-jishi/6-7.jpg)  
* 当有一个好的H:存在break point,有好的数据D:数据足够多（N够大），并且有好的A:选出够小的E<sub>in</sub>，就probably learned.

## Summary : Why Can Machines Learn?
---
由于no-free-lunch理论，我们是没有办法证明g在为学习的资料上与f到底有多接近的，所以如果我们要证明学习是可能的，必须在一个假设下：Hoeffding's Intequality

![](/img/linxuant-jishi/z-1.jpg)    

在N较大时，部分抽样的分布可以大概率上表示整体分布。

在这个前提下，我们知到，对于一个h大概率上E<sub>in</sub>接近E<sub>out</sub>，但是我们在集和H中挑选h，这么多h，难免会有某个h运气不好中了小概率事件E<sub>in</sub>和E<sub>out</sub>差距很大，如果我们的学习算法不行选中了这个h，就使得学习失败，那么在H中出现这样bad的h(可能一个可能多个，只要有这样的h就不行)的可能性有多大呢?

![](/img/linxuant-jishi/z-2.jpg)    

其中M是H中h的个数，由于exp项趋于0，所以当M有限时，整体概率趋于零，也就是说，在M有限时，发生上述情况的概率趋于零，即学习是可能的。

那么当M是无穷时这个概率又会是多少呢？

虽然我们说M是无穷大，但不是所有的h都满足H的条件，例如：

![](/img/linxuant-jishi/z-3.jpg)    

H是二维平面上所有的直线(也就是说这个问题就是线性可分问题，所以所有候选的h构成的H是直线)，图中画叉的两幅图，他们就不满足该条件，而对于N个点，他们所能构成的最多的满足条件的组合数(真实情况下可能产生的数据，因为该问题就是线性可分问题，所以真实情况下就不能产生图中划掉的那样的数据) = 有效的直线数量 = h的数量：

![](/img/linxuant-jishi/z-4.jpg)    

![](/img/linxuant-jishi/z-5.jpg)  

我们希望M可以被有效的N所替代，所以引入了成长函数：

![](/img/linxuant-jishi/z-6.jpg)  

它表示N个点最多可能的组合。

不同情况(问题)下成长函数不同，有的可以直接得到，有的则不行：

![](/img/linxuant-jishi/z-7.jpg)  

如果没有不符合条件的组合，那么成长函数m<sub>H</sub>(n)=2<sup>n</sup>，如果我们想让上面的概率趋于零，就希望可以找到成长函数的上界，从而引入了break point:

![](/img/linxuant-jishi/z-8.jpg)  

它是指第一个m<sub>H</sub>(k)=2<sup>k</sup>的点k

有了break point之后，我们定义bounding function B(N,k):

![](/img/linxuant-jishi/z-9.jpg)  

指在break point = k时，成长函数m<sub>H</sub>(n)的最大可能的值，也就是我们要找的成长函数的上界，可以证明：

![](/img/linxuant-jishi/z-10.jpg)  

也就是说，B(N,k)是有上界的，并且这个上界是多项式级的，所以当存在break point时，成长函数的上界B(N,k)有上界，即当有break point时，成长函数有多项式上界(多项式上界乘以趋于0的值最终还会趋于零)。

我们得到了成长函数有上界的结论，那么我们能不能把这个成长函数直接放到上面我们算的概率式子中，就想下图所示那样？

![](/img/linxuant-jishi/z-11.jpg)  

其实是不能直接得到这个式子的，但是我们经过数学推导可以得到下面的式子：

![](/img/linxuant-jishi/z-12.jpg)  

在N很大的前提下，可以得到上式，称为VC bound

所以我们可以得到结论：H中有无限h时，若成长函数存在break point，那么learning也是成立的











