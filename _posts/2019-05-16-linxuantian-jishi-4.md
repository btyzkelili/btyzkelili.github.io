---
layout:     post
title:      "林轩田-机器学习基石-Lecture4"
subtitle:   ""
date:       2019-05-16
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 一. When Can Machines Learn?
## Lecture 4: Feasibility of Learning
### 1.Learning is impossible?
* no-free-lunch：没有方法证明g在未学习资料上与f到底有多接近，除非加一些假设：
#### 1.1 预备知识
![](/img/linxuant-jishi/4-4.jpg)  
* Hoeffding's Inequslity  
	在N较大的时候，部分抽样的分布可以大概率上表示整体
* PAC:probably approximately correct  
#### 1.2 Prove Learning is possible 
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
#### 1.3 summary
* 1.挑出的珠子分布与整体分布相同 2.h的个数有限，满足以上两个条件，学习是可能的。（对于h个数很大的分析，见后面章节）