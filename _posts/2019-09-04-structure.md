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
已知F(x,y)函数，怎么找与x最匹配的y，我们先假设有方法可以做到

#### Problem3
![](/img/lhy_ml/structure-17.jpg)  
已知数据，如何训练F(x,y)

![](/img/lhy_ml/structure-18.jpg)  
![](/img/lhy_ml/structure-19.jpg)  
类似于感知机，我们以二维Φ为例，红色的圆点表示图片1正确的框法，蓝色表示图片1不正确的框法，红色星星表示图片2正确的框法，
蓝色星星表示图片2不正确的框法，红色的点是哪一个由problem2来找到，w是二维平面上的一条直线，我们要让不断更新w使得红色的w·Φ最大，
当w不再更新时即训练完成

