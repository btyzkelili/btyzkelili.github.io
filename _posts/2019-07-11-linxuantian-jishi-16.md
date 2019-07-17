---
layout:     post
title:      "林轩田-机器学习基石-笔记4"
subtitle:   ""
date:       2019-07-17 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 四. How Can Machines Learn Better?
---
## Lecture 13: Hazard of Overfitting
---
#### 13.1 What is Overfitting?

![](/img/linxuant-jishi/13-1.PNG)    

* overfitting产生的原因：1. 使用过大的d<sub>vc</sub> (多项式次数过多)2. 数据有噪声 3. 数据规模N有限

#### 13.2 The Role of Noise and Data Size

![](/img/linxuant-jishi/13-2.PNG)
![](/img/linxuant-jishi/13-3.PNG)        

* 我们的数据由10次多项式带有噪声得到(右图)，然后分别用2次多项式与10次多项式进行拟合(左图绿线与红线)，会发现2次多项式的E<sub>out</sub>要好很多

![](/img/linxuant-jishi/13-4.PNG)    

* 上图左是2次多项式的E<sub>in</sub>E<sub>out</sub>关系，右边是10次多项式，可以看到，在数据量小的情况下(灰色区域:过拟合区域)，即使10次的E<sub>in</sub>很小，它的E<sub>out</sub>与E<sub>in</sub>差距很大。可以看到上面的2次方和10次方其实都发生了过拟合(E<sub>in</sub>小但是E<sub>out</sub>大)，但是2次方E<sub>out</sub>更小，虽然知道数据是10次方产生的，但在有噪声情况下10此方的表现并不好，那是不是没有噪声的情况下10次方的表现就好了呢？

* 一般而言，R在数据量小的情况下总是表现更好的那一个。

![](/img/linxuant-jishi/13-5.PNG)
![](/img/linxuant-jishi/13-6.PNG)    

* 右图是没有噪声的50次方产生的数据，由2此方和3次方进行拟合，发现仍然是2此方的效果好。这是因为不是真正的没有噪声，目标非常复杂的时候，其实也是引入了一种噪声(用10次去拟合50次)

#### 13.3 Deterministic Noise

![](/img/linxuant-jishi/13-7.PNG)    

* 对于不同的noise level、N、目标的复杂度,可以得到如图的overfitting程度，可以看到，在N小的时候、stochastic(随机) noise大的时候，Determinstic noise(目标复杂度导致的)大的时候、最简单问题过复杂的表示(右图左下角)，都会overfitting

![](/img/linxuant-jishi/13-8.PNG)    

* determinstic noise: 它是目标f与H中的最好的h之间的差别，如右图灰色部分。表现和stochasitc noise一样，与计算机科学中使用的随机数思想相同(用纷杂的固定函数模拟随机数)

* 对于不同的H是不同的，对于给定的**x**是固定的

#### 13.4. Dealing whith Overfitting

![](/img/linxuant-jishi/13-9.PNG)    

* 我们如何解决overfitting问题呢？(对比开车)

1.从简单模型开始：开慢车

2.对数据进行处理cleaning/pruning: 使用更加准确的资料，跟准确的路况

3.找更多data：知道更多路

4.正则化：可以适时的踩刹车

5.仪表盘：时刻观察自己开车的情况怎么样

![](/img/linxuant-jishi/13-10.PNG)    

* 对于左上角的×，可以通过侦测，发现它离×很远，或者离o很近，发现它可能是一个有问题的点，可以将它改正确(data cleaning)，或者将它移除(data pruning)，这样的方法有可能有用，但是如果有很多点，有可能他的存在也并不会对最后的学习效果产生很大影响，但对有的问题可能会有较大影响

![](/img/linxuant-jishi/13-11.PNG)    

* 对于数字图片，我们将其移动或者旋转，不会影响他的真正含义，通过这种方法产生更多虚拟资料(data hinting)。

* 用这种方法要注意加进去的资料要有道理。

## Lecture 14: Regularization
---
#### 14.1 Regularized Hypothesis Set

![](/img/linxuant-jishi/14-1.PNG) 
![](/img/linxuant-jishi/14-2.PNG) 

我们希望能将右边的图(10次方)变成左边的图(2次方)，所以需要对右边的**w**进行限制，要求**w**<sub>3</sub>~**w**<sub>10</sub>=0，也就是说，我们"踩刹车"的方法是加限制。那么我们为什么不直接用二次呢，而是要对10次加上限制？这是为了有这样的思想来解下面的问题。

![](/img/linxuant-jishi/14-3.PNG) 

如果我们现在不是要**w**<sub>3</sub>~**w**<sub>10</sub>=0，而是在10此方中最多有三个**w**不是0其余全为0，这样如何求解？这个问题已经被证明是NP-hard，所以我们将其变换一下：

![](/img/linxuant-jishi/14-4.PNG) 

当**w**中大部分为0，所以每个w的平方和加起来也应该不大，我们让平方和小于一个常数C，有这样限制的H记为H(C)，通过这样softer限制的方法近似求解最多有3个w不是0的限制。

H(C)会随C增大而增大范围，当C无限大时，相当于没有限制，H(C)就和原来的10次方的H一样。

规则化H：加上条件的H

#### 14.2 Weight Decay Regularization

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

#### 14.3 Regularization and VC Theory

![](/img/linxuant-jishi/14-11.PNG)
![](/img/linxuant-jishi/14-12.PNG)  

看似VC Dimension变大了，但由于加了限制之后，我们实际上有效的VC Dimension其实变小了

#### 14.4 General Regularizers

![](/img/linxuant-jishi/14-14.PNG) 

选择regularizer的方法：

1.根据最终目标选择

2.选择自己认为合理的

3.选择容易优化好做的

![](/img/linxuant-jishi/14-13.PNG) 

L2是容易做优化的，L1是在做sparse时好用的

![](/img/linxuant-jishi/14-15.PNG) 

选择namda依赖于noise，更多的noise需要更大的namda(相当于路况不好的时候要常踩刹车)，但我们并不知道有多少noise，那么该如何选择呢？

## Lecture 15: Validation
---
#### 15.1 Model Selection Problem

![](/img/linxuant-jishi/15-1.PNG)   

* 如何做出选择？

* 模型选择：不可以画出图来视觉化选择，一是有的高纬度图像难以画出，二是自己大脑的VC就要算进去，所以最好不要通过视觉化来选择

![](/img/linxuant-jishi/15-2.PNG)   

* 用E<sub>in</sub>来选择是非常危险的，有可能导致overfitting或者模型复杂度很高，而我们手里没有D<sub>test</sub>，如果用了是非法的，所以我们将我们已有的资料分成两部分，一部分用来训练，一部分用来验证、选模型。

#### 15.2 Validation

![](/img/linxuant-jishi/15-3.PNG)   

* 流程：先将资料分成两部分，由训练及训练得到多个候选g<sub>1</sub><sup>-</sup>、g<sub>2</sub><sup>-</sup>...g<sub>M</sub><sup>-</sup>，然后用验证集进行验证，找出在验证集上表现最好的，然后再用所有数据进行训练。之所以最后要用所有数据进行训练，是因为我们直觉上认为跟多数据训练出的g要更好(learning curve)，我们可以通过实践证明这一点：

![](/img/linxuant-jishi/15-4.PNG)   

* 可以看到用验证机选出来后用全部数据再训练的g<sub>m</sub><sup>*</sup>(蓝线)表现要比单单用训练集训练出的g<sub>m</sub><sup>-</sup>(红线)更好

* 当验证集大小K增大时，会导致训练集变小，导致g<sub>m</sub><sup>-</sup>表现比用E<sub>in</sub>(所有数据做训练集，并用这些数据选择模型，黑色实线)做选择时还差，经验上，选择1/5作为验证集

#### 15.3 Leave-One-Out Cross Validation

![](/img/linxuant-jishi/15-5.PNG)   

* 如果我们希望E<sub>out</sub>(g)(用验证集挑选且最后用全部数据训练)近似E<sub>out</sub>(g<sup>-</sup>)(只用训练集训练)，那么要求验证集越小越好，如果我们希望E<sub>out</sub>(g<sup>-</sup>)和E<sub>val</sub>(g<sup>-</sup>)(用验证集挑选)近似，那么要求验证集越大越好

* 极端情况下，令K=1，loo=leave one  out，此时E<sub>loocv</sub>(每次留出一个点的平均错误)表现要远好于用E<sub>in</sub>

##3# 15.4 V-Fold Cross Validation

![](/img/linxuant-jishi/15-6.PNG)   

* 如果我们有很多数据，是很难算出E<sub>loocv</sub>的，并且用最后平均的方法难以消去每次选一个带来的错误的跳动，这两个原因导致leave one out实际情况下不太常用：所以我们习惯上把资料切成10份做交叉验证

![](/img/linxuant-jishi/15-7.PNG)   

* 通常情况下，V-fold要比一次验证要好，但是会付出计算的代价

* 训练集、验证集都是在选择模型，所以难以避免资料被污染，所以最后的测试集的表现要比验证集的差一些。

## Lecture 16: Three Learning Principles
---
#### 16.1 Occam's Razor(剃刀)

![](/img/linxuant-jishi/16-1.PNG)   

* 什么样叫做简单？为什么简单是好的？

* 简单的h: 视觉上看起来很简单，只需要少数的参数

* 简单的H: 有效的h不多就是简单的

* 简单的h与简单的H之间有联系

![](/img/linxuant-jishi/16-2.PNG)   

* 使用简单的模型能够解释资料，可以说资料是有一定的规律性，如果用很复杂的模型，无法辨别资料到底有没有规律性，因为复杂模型可以分开任何资料，所以用简单模型可以表现一定显著性。

* 先试线性模型，并且要注意，在使用模型时，要用自己想到的最简单的模型

#### 16.2 Sampling Bias

![](/img/linxuant-jishi/16-3.PNG)   

* 如果抽样有偏差，那学习也会有偏差，所以训练与测试要在同样的分布下，让训练环境与测试环境尽可能相似，如果测试是用时间上靠后的资料做测试，那么我们在训练的时候要强化时间上后面的数据，选验证集的时候不能随机抽样，而要用时间后面的去做验证集。

![](/img/linxuant-jishi/16-4.PNG)   

* 用银行现有的客户有没有刷爆信用卡的数据去训练，来预测新用户要不要给他信用卡，这个场景下，银行给的资料是之前系统决定要给信用卡的客户的数据，我们并不知道没给信用卡的客户会不会刷爆信用卡，用之前方法训练出的模型需要做一些调整，否则在真实情况下一个新用户到来时表现不会很好。

#### 16.3 Data Snooping(偷看)

* 视觉上肉眼偷看

![](/img/linxuant-jishi/16-5.PNG)   

* 用统计的方式间接偷看：在回归时如果要进行放缩，如果使用了test部分，影响了放缩过程，也算是偷眼看

![](/img/linxuant-jishi/16-6.PNG)   

* 根据别人的paper中用到的方法间接得知资料要选择怎样的模型会表现好，也算是一种偷看，而且在这些资料上表现好在真实情况下也不一定表现好

* 很难做到完全不偷看，通常折衷的方式是做小心使用验证，进行避免用资料做选择，做决定之前不要看资料，时时刻刻心存怀疑，到底经过多少过程得到结果，到底可能被污染的多严重。

#### 16.4 Power of Three

![](/img/linxuant-jishi/16-7.PNG)   

* 三个领域

![](/img/linxuant-jishi/16-8.PNG)   

* 三个理论限制

![](/img/linxuant-jishi/16-9.PNG)   

* 三个模型

![](/img/linxuant-jishi/16-10.PNG)   

* 三个有效的工具

![](/img/linxuant-jishi/16-11.PNG)   

* 三个学习原则

![](/img/linxuant-jishi/16-12.PNG)   

* 三个未来的方向

## Summary: How Can Machines Learn Better?

之前我们一直讨论E<sub>in</sub>要小但是不能太小，过小的E<sub>in</sub>却没有更好的E<sub>out</sub>这就是overfitting，导致overfitting的原因有哪些呢？  
![](/img/linxuant-jishi/13-7.PNG)    
可以看到，在N小的时候、stochastic(随机) noise大的时候，Determinstic noise(目标复杂度导致的)大的时候、最简单问题过复杂的表示(右图左下角)，都会overfitting

我们如何解决这个问题呢(对比开快车)？
1.从简单模型开始：开慢车
2.对数据进行处理cleaning/pruning: 使用更加准确的资料，跟准确的路况
3.找更多data：知道更多路
4.正则化：可以适时的踩刹车
5.仪表盘：时刻观察自己开车的情况怎么样

其中重要的方法：正则化

什么是正则化呢？正则化H就是加上条件的H，在这个加上条件的H下计算最小化的E<sub>in</sub>就是最小化E<sub>in</sub> + $\lambda$/N * **w**<sup>T</sup>**w**,其中参数$\lambda$越大，限制越强，表示希望**w**=0的越多，也就是H越小，更小的d<sub>EFF</sub>(有效的VC dimension)

那么我们如何选择这个限制/正则化呢？
1.根据最终目标选择
2.选择自己认为合理的
3.选择容易优化好做的
对于参数$\lambda$：
![](/img/linxuant-jishi/14-15.PNG) 
选择$\lambda$依赖于noise，更多的noise需要更大的$\lambda$(相当于路况不好的时候要常踩刹车)，但我们并不知道有多少noise，那么该如何选择呢？

由此引入了模型的选择话题，也就是使用验证集的使用：

我们从训练集中留出一部分数据,通常是2/5,作为验证集，通过验证集上模型表现的好坏来选择模型，选择完模型之后，应该将留出做验证集的数据放到模型里进行训练，保证充分利用数据(而且这样做的效果更好)。由于一次验证效果不一定好，所以我们可以多次验证:V-FoldCross-Validation，通常取v=10，但这样会带来计算上的代价





