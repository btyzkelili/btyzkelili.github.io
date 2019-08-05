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

#### 2.4 Summary
Deep Learning可以看作是先对x进行特征抽取/特征转换(隐层)，再进行机器学习步骤(输出层)，只不过特征转换是机器自己学，可以说是解问题的不同方法，有的问题也可以人工特征转换，但是一般语音图像常用Deep Learning

## 3. Why deep Learning?
#### 1. Modularization
![](/img/lhy_ml/why-0.png)  
理论上来说，只要神经元足够多，一层网络可以模拟任何函数，那为什么还要deep learning？虽然只用一层确实可以表示任何函数，但是要做到这件事会浪费参数没有效率，deep用更少的神经元可以做到相同的事，也就需要更少的参数，也就是需要更少的data，所以相同数据量、神经元情况下，Deep表现更好  

举例来说：  
![](/img/lhy_ml/why-1.png)  
![](/img/lhy_ml/why-2.png)  
直接用一层网络分类，长发男人的数据量少，训练效果可能不太好，但是多层网络，先去分男女、长短发，这两个的数据都不少，后面长发男人的分类器只要从前面得到男人+长发的结果就好，也就可以只用少量的数据但是训练的很好，所以，Deep -> Modularization，是更有效地使用参数和数据，相同神经元情况下，Deep要比单层网络表现更好，同时机器的modularization是自动学习的。

deep learning不是用大量的数据用复杂的网络硬train暴力碾压所以效果好，如果真的有无限多的数据，直接table loop up就好了，不用再用机器去学习，反而就是因为数据有限，才要让机器学习  

之前讲deep是先特征转换，与现在的modularization有什么联系呢？
![](/img/lhy_ml/why-3.png)  
特征转换相当于将折叠原来的数据空间，折叠后的一个点相当于原来的多个点，也就更有效的使用数据

#### 2. End-to-end Learning
![](/img/lhy_ml/why-4.png)  

#### 3. Complex Task
![](/img/lhy_ml/why-5.png)  
![](/img/lhy_ml/why-6.png)  
deep才可以让像的变不像，不像的变像，deep多层转换的时候，把原本不像的map到一起，也会把原来像的分开

