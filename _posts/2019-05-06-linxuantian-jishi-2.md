---
layout:     post
title:      "林轩田-机器学习基石-Lecture2"
subtitle:   ""
date:       2019-05-04 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 一. When Can Machines Learn?
## Lecture 2: Learning to Answer Yes/No
---  
### 1. Hypothesis Set: the 'Perceptron'
#### 1.1 linear formula h(x)
![](/img/linxuant-jishi/2-1.jpg)  
* h=hypothesis=perceptron(感知器)  
* h(x)计算向量x的得分-门槛值  
#### 1.2 Vector Form of Perceptron Hypothesis  
![](/img/linxuant-jishi/2-2.jpg)  
* **x<sub>0</sub>=1**  
* **w<sub>0</sub>=threshold**  
#### 1.3 Perceptrons in R<sup>2</sup>  
![](/img/linxuant-jishi/2-3.jpg)   
* 向量**x**=(x<sub>1</sub>,x<sub>2</sub>)：平面中的点  
* y：称为labels，一个特征向量x对应一个y,对应图中x或者o  
* h：平面中的线，线的一边为positive，另一边为negative  
#### 1.4 Select g from H(PLA)
* Perceptron Learning Algorithm(PLA)   
![](/img/linxuant-jishi/2-3.jpg)  
从**w**全为0的线开始，以某种顺序（正序、乱序等）找划分错误的点，根据该点修正**W**（图右侧向量转角方法:夹角为锐角向量乘积为正，直角为0，钝角为负），直到直线满足所有点。
* ![](/img/linxuant-jishi/2-5.jpg)   
**w**所示直线是划分直线h=**w<sup>t</sup>x**的法线,规定了原点之后，原点指向其他点的线即为该点的向量，因为向量之间锐角乘积为正，钝角为负，所以垂直于**w**向量的线是正负分界线，即每当确定一个**w**后，会产生一个分界线h，很多h(**x**)构成H，最终从H中选出最好的h去接近f
* Example
![](/img/linxuant-jishi/2-6.jpg)  
不选B原因：y<sub>n</sub>=0(?)  

#### 1.5 Some Remaining Issues of PLA
1. PLA一定会停止吗？  
	* necessary condition: Linear Separability(线性可分)
	* 假设线性可分，PLA会停下来（推导过程:02.pdf）
	* 向量内积：![](/img/linxuant-jishi/2-7.jpg)，正则化内积：两个向量内积越大离得越近，内积最大为1
2. 停止了一定正确吗？  

#### Learning with Noise Tolerance
* Pocket Algorithm  
![](/img/linxuant-jishi/2-7.jpg)  
线性可分用PLA,如果数据不是线性可分：PLA变形->Pocket，手里握着当前最好的线，比较下一条线是否更好，速度比PLA慢.

### 2. 总结
* 是非题：线性可分：PLA 非线性可分：Pockest Alorithm

