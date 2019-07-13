---
layout:     post
title:      "林轩田-机器学习基石-Lecture1"
subtitle:   ""
date:       2019-05-04 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
## 12. Nonlinear Transformation

### 12.1 Quadratic Hypotheses
![](/img/linxuant-jishi/12-1.png)     

* 之前讲的都是线性情况：s=**w<sup>T</sup>x**，每个w和x的一次方相乘后再加起来，得到的是一个将点划分成两半的直线，现在我们的点不在能用一条直线划分开，需要一个圈，所以我们进行特征转换feature transform，将x<sub>1</sub><sup>2</sup>对应z<sub>1</sub>，x<sub>2</sub><sup>2</sup>对应z<sub>2</sub>，这样在x空间的圈即可对应z空间的直线.

![](/img/linxuant-jishi/12-1.png)     

* 更进一步，z空间的线对应x空间特殊的曲线(圆、椭圆、双曲线等)，反之亦然。

![](/img/linxuant-jishi/12-1.png)     

* 将z空间进一步扩大，涵盖所有x的一次二次方，即可表示所有可能的曲线，所以只要在z空间里找到一条好的直线，就可以在x空间找到好的曲线。

### 12.2 Nonlinear Transform

![](/img/linxuant-jishi/12-4.png)  
![](/img/linxuant-jishi/12-5.png)      

* 首先，将x空间的点转换到z空间，然后在z空间好的直线，然后用x空间的点找到其在z空间的对应点，看看对应点在z空间直线的哪一边，来决定x空间的点是o还是×(而不是将z空间的直线转换为曲线，可能并不存在这样的转换)，这样就可以轻松完成suqduatic PLA\quadratic regression\cubic regression\polynomial regression...

![](/img/linxuant-jishi/12-6.png)     

* 关于特征转换，在之前讲过如何分辨手写数字是否为1，可以将图片特征转换为对称性等其他特征，来完成对判断，即把raw转换为concrete。

### 12.3 Price of Nonlinear Transform

![](/img/linxuant-jishi/12-7.png)     

* 进行特征转换之后，对需要存储大规模的向量，计算时也更加困难

![](/img/linxuant-jishi/12-8.png)     

* E<sub>in</sub>非常小的时候难以让E<sub>out</sub>与E<sub>in</sub>足够相似，而E<sub>out</sub>与E<sub>in</sub>足够相似时，E<sub>in</sub>又难以足够小

![](/img/linxuant-jishi/12-9.png)     

* 不要把自己视觉化或者大脑里得到的放到机器学习中(不要偷看数据)，不然会对自己的算法过于乐观，虽然在自己的推理下vc小，那是因为没有计算大脑里的vc。

### 12.4 Structured Hypothesis Sets

![](/img/linxuant-jishi/12-10.png)     

* H可以包含其他H，叫做H的structure

![](/img/linxuant-jishi/12-11.png)    

* H越大，vc越大，E<sub>in</sub>越小，但我们的目的并不是找到最小的E<sub>in</sub>，而是小的E<sub>out</sub>

![](/img/linxuant-jishi/12-12.png)     

* 先从线性模型开始，简单、有效、安全、而且一般表现都不错
