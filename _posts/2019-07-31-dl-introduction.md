---
layout:     post
title:      "Deep Learning"
subtitle:   "Introduction of Deep Learning"
date:       2019-07-31
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Deep Learning
---  
## 1. What's Deep
Deep = Many hidden layers，具体是多少层看自己理解，一般来说，用了NN方法都是deep learning

## 2. Step for Deep Learning
#### 2.1 function set
![](/img/lhy_ml/d-1.png)  
确定NN结构就是确定一个function set，参数确定的NN就是一个f，NN的输入是一个vector(一笔资料的多个feature，x<sup>n</sup>)，输出也是一个vector

![](/img/lhy_ml/d-2.png)  
可以通过GPU加速矩阵运算

![](/img/lhy_ml/d-3.png)  
如何设计NN结构？经验、直觉、尝试  
存在机器自己学习网络结构的方法，但是还没有普遍使用  

#### 2.2 Goodness of f
![](/img/lhy_ml/d-4.png)  
![](/img/lhy_ml/d-5.png)  
y=f(**x**)=σ(**w**<sup>L</sup>···σ(**w**<sup>1</sup>**x**+b<sup>1</sup>)···+b<sup>L</sup>)，根据每笔资料输出的y 与 target y 计算cross entropy 得到l，再把所有资料的l加起来得到L，L最小的f最好

#### 2.3 pick the best f
![](/img/lhy_ml/d-6.png)  
对L的每一个w(整个网络中所有的w)求微分，得到梯度∇L，用梯度下降更新w

## 3. Summary
Deep Learning可以看作是先对x进行特征抽取/特征转换(隐层)，再进行机器学习步骤(输出层)，只不过特征转换是机器自己学，可以说是解问题的不同方法，有的问题也可以人工特征转换，但是一般语音图像常用Deep Learning





