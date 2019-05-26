---
layout:     post
title:      "林轩田-机器学习基石-Lecture5"
subtitle:   ""
date:       2019-05-16
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 二. Why Can Machines Learn?
## Lecture 5: Training versus Testing
### 1.What's learning
![](/img/linxuant-jishi/5-1.jpg)  
* 把learning拆成两部分：  
	1. sure E<sub>in</sub> close to E<sub>out</sub>?  
	2. E<sub>in</sub> small enough?  
* 当M小的时候，坏事发生的概率小，满足条件1，但是可选的h少，不一定能找出足够小的E<sub>in</sub>，不满足条件2；当M大的时候，坏事发生的概率大，不满足条件1，但是可选的h多，可找出足够小的E<sub>in</sub>，满足条件2，由此得知M的重要性
* Example
![](/img/linxuant-jishi/5-2.jpg)  
### 2.M
![](/img/linxuant-jishi/5-3.jpg)  
* M:不同h的个数
### 3.Growth Function
![](/img/linxuant-jishi/5-4.jpg)  
* 在二维平面所有点上的划分h(直线)个数有无数个，从所有点中选出N个dichotomies(二分):H(**x**<sub>1</sub>,**x**<sub>2</sub>,...,**x**<sub>N</sub>)，在这N个点上的h最多有2<sup>N</sup>个(因为每个点不是o就是x两种情况)
![](/img/linxuant-jishi/5-5.jpg)  
* 将dichotomies:H(**x**<sub>1</sub>,**x**<sub>2</sub>,...,**x**<sub>N</sub>)的最大值看做m<sub>H</sub>(N):成长函数
### 4. M Replaced by Growth Function
#### 4.1 What if m<sub>H</sub>(N) replaces M?
![](/img/linxuant-jishi/5-6.jpg)  
* 不同情况下的m<sub>H</sub>(N)：  
![](/img/linxuant-jishi/5-7.jpg)    
* 当m<sub>H</sub>(N)是polynomial（多项式）时，不等式右边在N足够大时趋于0，当m<sub>H</sub>(N)是exponential（指数函数）时，不等式右边不趋于0
#### 4.2 Break Point of H
![](/img/linxuant-jishi/5-8.jpg)    
* break point:第一个m<sub>H</sub>(k)<2<sup>k</sup>的点k
几种情况下的break point:
![](/img/linxuant-jishi/5-8.jpg)    
* 如果没有break point:m<sub>H</sub>(N)=2<sup>N</sup>
* 如果有break point k:m<sub>H</sub>(N)=O(N<sup>k-1</sup>)(下一节证明)
