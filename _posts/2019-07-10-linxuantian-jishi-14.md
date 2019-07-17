---
layout:     post
title:      "林轩田-机器学习基石-Lecture14"
subtitle:   ""
date:       2019-07-10 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
## 14. Regularization

### 14.1 Regularized Hypothesis Set

![](/img/linxuant-jishi/14-1.PNG) 
![](/img/linxuant-jishi/14-2.PNG) 

我们希望能将右边的图(10次方)变成左边的图(2次方)，所以需要对右边的**w**进行限制，要求**w**<sub>3</sub>~**w**<sub>10</sub>=0，也就是说，我们"踩刹车"的方法是加限制。那么我们为什么不直接用二次呢，而是要对10次加上限制？这是为了有这样的思想来解下面的问题。

![](/img/linxuant-jishi/14-3.PNG) 

如果我们现在不是要**w**<sub>3</sub>~**w**<sub>10</sub>=0，而是在10此方中最多有三个**w**不是0其余全为0，这样如何求解？这个问题已经被证明是NP-hard，所以我们将其变换一下：

![](/img/linxuant-jishi/14-4.PNG) 

当**w**中大部分为0，所以每个w的平方和加起来也应该不大，我们让平方和小于一个常数C，有这样限制的H记为H(C)，通过这样softer限制的方法近似求解最多有3个w不是0的限制。

H(C)会随C增大而增大范围，当C无限大时，相当于没有限制，H(C)就和原来的10次方的H一样。

规则化H：加上条件的H

### 14.2 Weight Decay Regularization

![](/img/linxuant-jishi/14-5.PNG) 
![](/img/linxuant-jishi/14-6.PNG) 

我们现在要求最小的E<sub>in</sub>在上述条件下，其中 w的平方和=**w**<sup>T</sup>**w**，也就是w在半径为根号C的球中，之前推导过，减小E<sub>in</sub>就是向着梯度的反方向走(梯度方向是增长最快的方向)，当梯度反方向与球的法线(法线就是**w**)不平行时，如图，我们可以向着绿色箭头的方向移动，这样既可以减小E<sub>in</sub>也同时满足限制，直到我们移动到了梯度反方向与球的法线平行的位置，就是满足限制下的E<sub>in</sub>最小的点(?)

![](/img/linxuant-jishi/14-7.PNG) 
![](/img/linxuant-jishi/14-8.PNG) 

求解

![](/img/linxuant-jishi/14-9.PNG) 

一点namda就可以做到非常大的效果

可以得到结论：更大的namda，就是希望越少的w不为零，也就是限制更小的C

![](/img/linxuant-jishi/14-10.PNG) 

legendre Polynomials：不同此方之间相互垂直(?)

### 14.3 Regularization and VC Theory

![](/img/linxuant-jishi/14-11.PNG)
![](/img/linxuant-jishi/14-12.PNG)  

看似VC Dimension变大了，但由于加了限制之后，我们实际上有效的VC Dimension其实变小了

### 14.4 General Regularizers

![](/img/linxuant-jishi/14-14.PNG) 

选择regularizer的方法：

1.根据最终目标选择

2.选择自己认为合理的

3.选择容易优化好做的

![](/img/linxuant-jishi/14-13.PNG) 

L2是容易做优化的，L1是在做sparse时好用的

![](/img/linxuant-jishi/14-15.PNG) 

选择namda依赖于noise，更多的noise需要更大的namda(相当于路况不好的时候要常踩刹车)，但我们并不知道有多少noise，那么该如何选择呢？


