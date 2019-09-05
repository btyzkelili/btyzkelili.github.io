---
layout:     post
title:      "Structure Learning"
subtitle:   "Introduction"
date:       2019-09-04
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - SVM
---  
## Structure Learning
![](/img/lhy_ml/structure-1.jpg)  
之前的模型都是输入一个vector输出另一个vector，现在输入和输出可能是其他形式：Sequence,tree structure,
bounding box,paragraph等

Structure Learning的unified形式，训练时，F的输入是X,Y，输出常数R，让匹配的X,的R尽可能大，测试时，输入X找让F(x,y)
结果最大的y(穷举所有y)，也就是和x最匹配的y

![](/img/lhy_ml/structure-2.jpg)  
有一个任务是在图片中圈出人物"Haruhi"训练时，让正确的图片圈法分数最高，测试时，穷举所有圈的方法，找到得分最高的圈发

其他任务举例：  
![](/img/lhy_ml/structure-3.jpg)  
![](/img/lhy_ml/structure-4.jpg)  

可以看做是几率形式：  
![](/img/lhy_ml/structure-5.jpg)  
![](/img/lhy_ml/structure-6.jpg)  
几率形式有一定缺点，有的时候任务说成几率有些奇怪，而且几率有限制1，需要花时间normalization，但几率容易想象理解

![](/img/lhy_ml/structure-7.jpg)  
![](/img/lhy_ml/structure-8.jpg)  
![](/img/lhy_ml/structure-9.jpg)  
![](/img/lhy_ml/structure-10.jpg)  
要想做到Structure Learning需要解决上面三个问题

![](/img/lhy_ml/structure-11.jpg)  
对比DNN，DNN是Structure Learning的特例，图中CE指cross entropy

## Structured Linear Model
#### Problem 1
![](/img/lhy_ml/structure-12.jpg)  
如果F(x,y)有特殊的形式，那么第三个就不是问题

![](/img/lhy_ml/structure-13.jpg)  
这个特殊的形式是F(x,y)=w·Φ(内积)，Φ是(x,y)的特征向量，可以自己定，解决问题1主要就是想办法定义Φ

![](/img/lhy_ml/structure-14.jpg)  
举例来说，(图片x，框y)的属性Φ可以=[图片中框内红色的比例，...]

![](/img/lhy_ml/structure-15.jpg)  
因为F(x,y)是一个线性模型不能做很复杂的事，可以人工找feature，也可以用深度网络来学习得到Φ

#### Problem2
![](/img/lhy_ml/structure-16.jpg)  
已知F(x,y)函数，怎么穷举y找与x最匹配的y，这个问题任务相关的，需要自己找办法解决，我们先假设有方法可以做到

#### Problem3
![](/img/lhy_ml/structure-17.jpg)  
已知数据，如何训练F(x,y)

![](/img/lhy_ml/structure-18.jpg)  
![](/img/lhy_ml/structure-19.jpg)  
上面的算法叫做Structure Percepreon，类似于感知机，我们以二维Φ为例，红色的圆点表示图片1正确的框法，蓝色表示图片1不正确的框法，红色星星表示图片2正确的框法，
蓝色星星表示图片2不正确的框法，红色的点是哪一个由problem2来找到，w是二维平面上的一条直线，我们要让不断更新w使得红色的w·Φ最大，当w不再更新时即训练完成

![](/img/lhy_ml/structure-20.jpg)  
在可分情况下，最多(R/δ)<sup>2</sup>次更新算法会结束，其中δ是红色点比蓝色点与w的内积至少要大δ，R：同一个x与不同y会得到不同的feature vector Φ，这些Φ之间距离的最大值就是R，所以更新次数与蓝色点的数量/y的数量无关（视频课程中有数学证明）

**How to make training fast?**
![](/img/lhy_ml/structure-21.jpg)  
增大δ，找一组好的feature让蓝色和红色分的更开，如果仅仅是将feature* 2，δ会增大但是R也会增大，更新次数上限不会改变，但是真实情况下，很少有问题的feature是separable，我们自己也很难找到separable的feature表示，所以接下来研究Non-separable case

**Defining Cost Function**
![](/img/lhy_ml/structure-22.jpg)  
Cost Function=∑我们得到的w认为与x最匹配的y的Φ 与 w的内积-真正最好的y的内积，C的最小值=0，之所以是只用最w认为最好的来算而不是用前三之类的，是因为我们再问题2中假设可以解出最好的，而用前三会给自己找麻烦

**SGD**
![](/img/lhy_ml/structure-23.jpg)  
我们用(Stochastic) Gradient Descent对C进行更新
![](/img/lhy_ml/structure-24.jpg)  
以w二维为例，w空间被max切割，w落在左下角,argmax[w·Φ] = y'，在某一个region里C<sup>n</sup>可以容易得到，而此时的C<sup>n</sup>容易计算微分，能计算出微分也就可以用SGD更新
![](/img/lhy_ml/structure-25.jpg)  
argmax:返回后面式子取最大值时的参数值

**Another Cost Function**
![](/img/lhy_ml/structure-26.jpg)  
不同错误之间也有好坏之分，右边的模型比较安全，如果train data和test data有一定差距，第一名不是正确的，右边模型可以保证分数高的和第一名差距不大

![](/img/lhy_ml/structure-27.jpg)  
定义两个y之间的差距是任务相关的，要自己定义，常见的定法与右下角，其中A(y)表示y框出的面积

![](/img/lhy_ml/structure-28.jpg)  
![](/img/lhy_ml/structure-29.jpg)  
找有Δy的problem2需要自己想办法解，设计容易解的Δy

![](/img/lhy_ml/structure-30.jpg)  
![](/img/lhy_ml/structure-31.jpg)  
最小化上面新的cost function其实是最小化在训练集上的错误的upper bound，以为新cost function求的是max，这个upper bound变小不代表error变小，但error有可能变小，所以我们希望是C'更小，但是C'很难去minimize，因为y可以取任意值而且Δ可以是任何函数，不过C是C'的上界，我们让C最小也就让C'最小(视频中有证明为什么C是C'上界)

**Regularization**
![](/img/lhy_ml/structure-32.jpg)  ![](/img/lhy_ml/structure-33.jpg)  

## Structred SVM
![](/img/lhy_ml/structure-34.jpg)  
在minimize C<sup>n</sup>的情况下第二个式子和第三个式子相等
![](/img/lhy_ml/structure-35.jpg)  
![](/img/lhy_ml/structure-36.jpg)  
![](/img/lhy_ml/structure-37.jpg)  
![](/img/lhy_ml/structure-38.jpg)  
![](/img/lhy_ml/structure-39.jpg)  
可以从SVM package中找solver来解决问题，在是式子中有太多限制，我们需要进行改进

**Cutting Plane Algorithm**
