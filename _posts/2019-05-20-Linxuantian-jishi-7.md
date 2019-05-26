---
layout:     post
title:      "林轩田-机器学习基石-Lecture7"
subtitle:   ""
date:       2019-05-20
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 二. Why Can Machines Learn?
## Lecture 7: The VC Dimension
### 1.VC Dimension Definition
![](/img/linxuant-jishi/7-1.jpg)  
* d<sub>vc</sub>=minimum breakpoint-1 （最大的non-break point） 
* 好的H:d<sub>vc</sub> is finite  
![](/img/linxuant-jishi/7-2.jpg) 
在d<sub>vc</sub>有限的情况下：
* 不管A选了一个大的E<sub>in</sub>还是小的E<sub>in</sub>，E<sub>in</sub>都近似E<sub>out</sub> 
* 不论数据X的分布P是怎样的
* 不论目标函数是怎样的
### 2.VC Dimension of Perceptrons
![](/img/linxuant-jishi/7-3.jpg) 
* d<sub>VC</sub>=d(perceptron维度)+1  
![](/img/linxuant-jishi/7-5.jpg) 
![](/img/linxuant-jishi/7-4.jpg) 
* VC dimension<==>perceptron dimension：hypothesis是由**w**表示的，这些**w**是hypothsis的自由度，类比可以调的旋钮
* VC dimension:在二元分类时有多少自由度，衡量自由度告诉我们H到底好不好
* VC dimension物理意义：H有多少可以调的旋钮（自由度），可以估计H复杂度，以此来决定用多少资料。
![](/img/linxuant-jishi/7-6.jpg) 
### 3.VC Bound REphrase
#### 3.1 Penalty for Model Complexity
![](/img/linxuant-jishi/7-7.jpg) 
* 通过对VC Bound进行变换，可以得到如上结果，发现一味追求小的E<sub>in</sub>（强的H）不一定得到好的E<sub>out</sub>，要同时到考虑到模型复杂付出的代价，最好的d<sub>VC</sub>在中间。
#### 3.2 Sample Complexity
![](/img/linxuant-jishi/7-8.jpg) 
* VC Bound对资料复杂度:理论上需要1万倍的d<sub>VC</sub>，但实际上N大约为10倍的d<sub>VC</sub>就可取到比较好的效果,可以看到VC Bound非常宽松
#### 3.3 Looseness of VC Bound
![](/img/linxuant-jishi/7-9.jpg) 
* VC Bound很宽松，但我们设计机器学习演算法时用到的不是它严格的部分（例如3.2提到的理论上使用1万倍的d<sub>VC</sub>），而是他表现出的哲学信息（例如3.1提到的不要一味追求最强的H）。
## 4. Summary
* Learning happens if finite d<sub>VC</sub>,large N, and low E<sub>in</sub>

