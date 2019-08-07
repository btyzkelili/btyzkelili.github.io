---
layout:     post
title:      "Unsupervised Learning"
subtitle:   "Linear Methods"
date:       2019-08-07
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Unsupervised Learning
---  
## 1.Introduction
![](/img/lhy_ml/uslm-1.png)  
无监督学习有两种情况：化繁为简（clustering、Dimension Reduction） 和 无中生有

## 2.Clustering
#### K-means
![](/img/lhy_ml/uslm-2.png)  
具体要分多少类需要经验上决定，最好用已有的数据作为初始中心，防止出现某一类没有资料的情况

#### HAC
![](/img/lhy_ml/uslm-3.png)  
可以不用事先决定要分多少类

## 3.Distribute Representation
![](/img/lhy_ml/uslm-4.png)  

### PCA
![](/img/lhy_ml/uslm-5.png)  
![](/img/lhy_ml/uslm-6.png)  
我们把x转换成低维度的z，z1=w1·x表示求x在w1上的投影，也就是在w1轴上的值，同时我们希望在轴上的值分布尽可能开，也就是Var(z1)要大，要转换成多个维度，
就用多个w1,w2,...，具体要转换到多少维，要自己规定，同时，w之间要正交(防止找到的w之间有重合)，最后得到W是一个正交矩阵

求解PCA/W:  
![](/img/lhy_ml/uslm-7.png)  
x可以看作是由很多component={u1,u2,...}组成，也就是x = c1u1+c2u2+...+x<sup>-</sup>  
![](/img/lhy_ml/uslm-8.png)  
L要求每一笔资料x的 x-x<sup>-</sup> 和 由component组成的结果 尽可能相同，对比前面PCA，{w1,w2,...}={u1,u2,...}，求解W就是求解U
![](/img/lhy_ml/uslm-9.png)  
![](/img/lhy_ml/uslm-10.png)  
用SVD矩阵分解方法求使得L最小的U，得到的U就是component也就是PCA的解W，总的来说，就是将x-x<sup>-</sup>进行矩阵分解，得到的U就是x-x<sup>-</sup>的
降维的维度/重要的特征

#### auto-encoder 
![](/img/lhy_ml/uslm-11.png)  
因为x-x<sup>-</sup> = c1u1+c2u2+...(1)，所以ck=(x-x<sup>-</sup>)wk(2)，输入x-x<sup>-</sup>得到ck(2)，再通过ck得到x(1)，让输出的x hat与
输入尽可能相同，构成了auto-encoder

#### Weakness of PCA
![](/img/lhy_ml/uslm-12.png)  

#### Application
![](/img/lhy_ml/uslm-13.png)  
推荐系统：上图是人物A\B\C...购买各个玩偶的数量，用矩阵分解可以得到人物和玩偶在2个(可以自己定)维度上的值，也就是他们在这两个特点上的值(可能是天然呆、
傲娇)上的值，分析他们在低纬度上的表现，可以看到各自的特点(人物喜欢天然呆、玩偶是天然呆类型等)，也可以用得到表格中没有的值，来对人物进行推荐。
![](/img/lhy_ml/uslm-14.png)  
如果表格中有没有的值，也可以用gradient descent只计算有的值，进行计算

![](/img/lhy_ml/uslm-15.png)  
LSA方法类似，得到的特征可能是topic等

![](/img/lhy_ml/uslm-16.png)  



