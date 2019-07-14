---
layout:     post
title:      "林轩田-机器学习基石-Lecture15"
subtitle:   ""
date:       2019-07-10 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
## 15. Validation

### 15.1 Model Selection Problem

![](/img/linxuant-jishi/15-1.PNG)   

* 如何做出选择？

* 模型选择：不可以画出图来视觉化选择，一是有的高纬度图像难以画出，二是自己大脑的VC就要算进去，所以最好不要通过视觉化来选择

![](/img/linxuant-jishi/15-2.PNG)   

* 用E<sub>in</sub>来选择是非常危险的，有可能导致overfitting或者模型复杂度很高，而我们手里没有D<sub>test</sub>，如果用了是非法的，所以我们将我们已有的资料分成两部分，一部分用来训练，一部分用来验证、选模型。

### 15.2 Validation

![](/img/linxuant-jishi/15-3.PNG)   

* 流程：先将资料分成两部分，由训练及训练得到多个候选g<sub>1</sub><sup>-</sup>、g<sub>2</sub><sup>-</sup>...g<sub>M</sub><sup>-</sup>，然后用验证集进行验证，找出在验证集上表现最好的，然后再用所有数据进行训练。之所以最后要用所有数据进行训练，是因为我们直觉上认为跟多数据训练出的g要更好(learning curve)，我们可以通过实践证明这一点：

![](/img/linxuant-jishi/15-4.PNG)   

* 可以看到用验证机选出来后用全部数据再训练的g<sub>m</sub><sup>*</sup>(蓝线)表现要比单单用训练集训练出的g<sub>m</sub><sup>-</sup>(红线)更好

* 当验证集大小K增大时，会导致训练集变小，导致g<sub>m</sub><sup>-</sup>表现比用E<sub>in</sub>(所有数据做训练集，并用这些数据选择模型，黑色实线)做选择时还差，经验上，选择1/5作为验证集

### 15.3 Leave-One-Out Cross Validation

![](/img/linxuant-jishi/15-5.PNG)   

* 如果我们希望E<sub>out</sub>(g)(用验证集挑选且最后用全部数据训练)近似E<sub>out</sub>(g<sup>-</sup>)(只用训练集训练)，那么要求验证集越小越好，如果我们希望E<sub>out</sub>(g<sup>-</sup>)和E<sub>val</sub>(g<sup>-</sup>)(用验证集挑选)近似，那么要求验证集越大越好

* 极端情况下，令K=1，loo=leave one  out，此时E<sub>loocv</sub>(每次留出一个点的平均错误)表现要远好于用E<sub>in</sub>

### 15.4 V-Fold Cross Validation

![](/img/linxuant-jishi/15-6.PNG)   

* 如果我们有很多数据，是很难算出E<sub>loocv</sub>的，并且用最后平均的方法难以消去每次选一个带来的错误的跳动，这两个原因导致leave one out实际情况下不太常用：所以我们习惯上把资料切成10份做交叉验证

![](/img/linxuant-jishi/15-7.PNG)   

* 通常情况下，V-fold要比一次验证要好，但是会付出计算的代价

* 训练集、验证集都是在选择模型，所以难以避免资料被污染，所以最后的测试集的表现要比验证集的差一些。








