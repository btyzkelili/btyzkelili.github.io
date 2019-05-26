---
layout:     post
title:      "林轩田-机器学习基石-Lecture6"
subtitle:   ""
date:       2019-05-19
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 二. Why Can Machines Learn?
## Lecture 6: Theory of Generalization
### 1.Restriction of Break Point
* grow function:m<sub>H</sub>(N) N个点上最多可以产生多少种满足H的点的划分方式(dichotomies点的ox组合)  
* break point=k:当N=k时，成长函数第一次!=2<sup>k</sup>,意味着在有n>=k个点时，这些点中任意k个都不能shatter(shatter:k个点有2<sup>k</sup>种所有的ox组合)  
![](/img/linxuant-jishi/6-1.jpg)  
* 对于上图：k=2，说明在点的个数N=2时，这2个点不可以组合出2<sup>2</sup>种所有ox情况，因为存在某些情况不能满足H（break point定义），同理，当N>2时，不会出现任意2个点它们的组合为2<sup>2</sup>种所有的排序情况，所以当N=3时，最多有5种划分这3个点的方式，即5 dichotomies。
### 2.Bounding Function
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
### 3.Vapnik-Chervonenkis(VC)bound
![](/img/linxuant-jishi/6-7.jpg)  
* 前一章提到的M可以被成长函数替代，并且经过三步证明（略）后可以得到VC bound，证明了E<sub>in</sub>和E<sub>out</sub>相差很大的概率，在成长函数有break point、N足够大时时，趋于0.  
* 到此，证明了H中有无限h时，若成长函数存在break point，那么learning也是成立的  
![](/img/linxuant-jishi/6-7.jpg)  
* 当有一个好的H:存在break point,有好的数据D:数据足够多（N够大），并且有好的A:选出够小的E<sub>in</sub>，就probably learned.