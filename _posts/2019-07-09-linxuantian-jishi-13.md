---
layout:     post
title:      "林轩田-机器学习基石-Lecture13"
subtitle:   ""
date:       2019-05-04 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
## 13. Hazard of Overfitting

### 13.1 What is Overfitting?

![](/img/linxuant-jishi/13-1.png)    

* overfitting产生的原因：1. 使用过大的d<sub>vc</sub> (多项式次数过多)2. 数据有噪声 3. 数据规模N有限

### 13.2 The Role of Noise and Data Size

![](/img/linxuant-jishi/13-2.png)
![](/img/linxuant-jishi/13-3.png)        

* 我们的数据由10次多项式带有噪声得到(右图)，然后分别用2次多项式与10次多项式进行拟合(左图绿线与红线)，会发现2次多项式的E<sub>out</sub>要好很多

![](/img/linxuant-jishi/13-4.png)    

* 上图左是2次多项式的E<sub>in</sub>E<sub>out</sub>关系，右边是10次多项式，可以看到，在数据量小的情况下(灰色区域:过拟合区域)，即使10次的E<sub>in</sub>很小，它的E<sub>out</sub>与E<sub>in</sub>差距很大。可以看到上面的2次方和10次方其实都发生了过拟合(E<sub>in</sub>小但是E<sub>out</sub>大)，但是2次方E<sub>out</sub>更小，虽然知道数据是10次方产生的，但在有噪声情况下10此方的表现并不好，那是不是没有噪声的情况下10次方的表现就好了呢？

* 一般而言，R在数据量小的情况下总是表现更好的那一个。

![](/img/linxuant-jishi/13-5.png)
![](/img/linxuant-jishi/13-6.png)    

* 右图是没有噪声的50次方产生的数据，由2此方和3次方进行拟合，发现仍然是2此方的效果好。这是因为不是真正的没有噪声，目标非常复杂的时候，其实也是引入了一种噪声(用10次去拟合50次)

### 13.3 Deterministic Noise

![](/img/linxuant-jishi/13-7.png)    

* 对于不同的noise level、N、目标的复杂度,可以得到如图的overfitting程度，可以看到，在N小的时候、stochastic(随机) noise大的时候，Determinstic noise(目标复杂度导致的)大的时候、最简单问题过复杂的表示(右图左下角)，都会overfitting

![](/img/linxuant-jishi/13-8.png)    

* determinstic noise: 它是目标f与H中的最好的h之间的差别，如右图灰色部分。表现和stochasitc noise一样，与计算机科学中使用的随机数思想相同(用纷杂的固定函数模拟随机数)

* 对于不同的H是不同的，对于给定的**x**是固定的

### 13.4. Dealing whith Overfitting

![](/img/linxuant-jishi/13-9.png)    

* 我们如何解决overfitting问题呢？(对比开车)

1.从简单模型开始：开慢车

2.对数据进行处理cleaning/pruning: 使用更加准确的资料，跟准确的路况

3.找更多data：知道更多路

4.正则化：可以适时的踩刹车

5.仪表盘：时刻观察自己开车的情况怎么样

![](/img/linxuant-jishi/13-10.png)    

* 对于左上角的×，可以通过侦测，发现它离×很远，或者离o很近，发现它可能是一个有问题的点，可以将它改正确(data cleaning)，或者将它移除(data pruning)，这样的方法有可能有用，但是如果有很多点，有可能他的存在也并不会对最后的学习效果产生很大影响，但对有的问题可能会有较大影响

![](/img/linxuant-jishi/13-11.png)    

* 对于数字图片，我们将其移动或者旋转，不会影响他的真正含义，通过这种方法产生更多虚拟资料(data hinting)。

* 用这种方法要注意加进去的资料要有道理。
