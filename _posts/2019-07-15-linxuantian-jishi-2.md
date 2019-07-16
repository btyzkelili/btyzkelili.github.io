---
layout:     post
title:      "林轩田-机器学习基石-笔记2"
subtitle:   ""
date:       2019-07-13 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 二. Why Can Machines Learn?
---
## Lecture 5: Training versus Testing
---
#### 5.1 What's learning
![](/img/linxuant-jishi/5-1.jpg)  
* 把learning拆成两部分：  
	1. sure E<sub>in</sub> close to E<sub>out</sub>?  
	2. E<sub>in</sub> small enough?  
* 当M小的时候，坏事发生的概率小，满足条件1，但是可选的h少，不一定能找出足够小的E<sub>in</sub>，不满足条件2；当M大的时候，坏事发生的概率大，不满足条件1，但是可选的h多，可找出足够小的E<sub>in</sub>，满足条件2，由此得知M的重要性
* Example  
![](/img/linxuant-jishi/5-2.jpg) 
 
#### 5.2 M
![](/img/linxuant-jishi/5-3.jpg)  
* M:不同h的个数

#### 5.3 Growth Function
![](/img/linxuant-jishi/5-4.jpg)  
* 在二维平面所有点上的划分h(直线)个数有无数个，从所有点中选出N个dichotomies(二分):H(**x**<sub>1</sub>,**x**<sub>2</sub>,...,**x**<sub>N</sub>)，在这N个点上的h最多有2<sup>N</sup>个(因为每个点不是o就是x两种情况)  
![](/img/linxuant-jishi/5-5.jpg)  
* 将dichotomies:H(**x**<sub>1</sub>,**x**<sub>2</sub>,...,**x**<sub>N</sub>)的最大值看做m<sub>H</sub>(N):成长函数

#### 5.4 M Replaced by Growth Function
##### 5.4.1 What if m<sub>H</sub>(N) replaces M?
![](/img/linxuant-jishi/5-6.jpg)  
* 不同情况下的m<sub>H</sub>(N)：  
![](/img/linxuant-jishi/5-7.jpg)    
* 当m<sub>H</sub>(N)是polynomial（多项式）时，不等式右边在N足够大时趋于0，当m<sub>H</sub>(N)是exponential（指数函数）时，不等式右边不趋于0
##### 5.4.2 Break Point of H
![](/img/linxuant-jishi/5-8.jpg)    
* break point:第一个m<sub>H</sub>(k)<2<sup>k</sup>的点k    
* 如果没有break point:m<sub>H</sub>(N)=2<sup>N</sup>
* 如果有break point k:m<sub>H</sub>(N)=O(N<sup>k-1</sup>)(下一节证明)

## Lecture 6: Theory of Generalization
---
#### 6.1 Restriction of Break Point
* grow function:m<sub>H</sub>(N) N个点上最多可以产生多少种满足H的点的划分方式(dichotomies点的ox组合)  
* break point=k:当N=k时，成长函数第一次!=2<sup>k</sup>,意味着在有n>=k个点时，这些点中任意k个都不能shatter(shatter:k个点有2<sup>k</sup>种所有的ox组合)  
![](/img/linxuant-jishi/6-1.jpg)  
* 对于上图：k=2，说明在点的个数N=2时，这2个点不可以组合出2<sup>2</sup>种所有ox情况，因为存在某些情况不能满足H（break point定义），同理，当N>2时，不会出现任意2个点它们的组合为2<sup>2</sup>种所有的排序情况，所以当N=3时，最多有5种划分这3个点的方式，即5 dichotomies。

#### 6.2 Bounding Function
![](/img/linxuant-jishi/6-2.jpg)  
* bounding funtion B(N,k):在N个点上任意k个点no shatter所能得到的满足H的最多划分方式  
![](/img/linxuant-jishi/6-4.jpg)  
* 当k=1,因为只要超过一划分方式就会有某个点的ox值与第一种划分不同，此时该点shatter，不满足k=1条件，所以B(N,1)=1  
* 当k>N，因为k个点no shtter，而N<k，所以这N个点可以shatter，所以最多有2<sup>N</sup>种点的组合方式。  
* 当k=N，因为不能有N个点shatter，所以最多有2<sup>N</sup>-1种点的组合方式。  
* 其他，![](/img/linxuant-jishi/6-5.jpg)，证明略   

由此得到B(N,k)的上限是有关N的多项式：  
![](/img/linxuant-jishi/6-6.jpg)  
* 当k确定时，B(N,k)被上限多形式poly(N)限制，所以：如果break point存在，成长函数是多项式级。   

#### 6.3 Vapnik-Chervonenkis(VC)bound
![](/img/linxuant-jishi/6-7.jpg)  
* 前一章提到的M可以被成长函数替代，并且经过三步证明（略）后可以得到VC bound，证明了E<sub>in</sub>和E<sub>out</sub>相差很大的概率，在成长函数有break point、N足够大时时，趋于0.  
* 到此，证明了H中有无限h时，若成长函数存在break point，那么learning也是成立的  
![](/img/linxuant-jishi/6-8.jpg)  
* 当有一个好的H:存在break point,有好的数据D:数据足够多（N够大），并且有好的A:选出够小的E<sub>in</sub>，就probably learned.

## Lecture 7: The VC Dimension
#### 7.1 VC Dimension Definition
![](/img/linxuant-jishi/7-1.jpg)  
* d<sub>vc</sub>=minimum breakpoint-1 （最大的non-break point） 
* 好的H:d<sub>vc</sub> is finite  
![](/img/linxuant-jishi/7-2.jpg) 
在d<sub>vc</sub>有限的情况下：
* 不管A选了一个大的E<sub>in</sub>还是小的E<sub>in</sub>，E<sub>in</sub>都近似E<sub>out</sub> 
* 不论数据X的分布P是怎样的
* 不论目标函数是怎样的
#### 7.2 VC Dimension of Perceptrons
![](/img/linxuant-jishi/7-3.jpg) 
* d<sub>VC</sub>=d(perceptron维度)+1  
![](/img/linxuant-jishi/7-5.jpg) 
![](/img/linxuant-jishi/7-4.jpg) 
* VC dimension<==>perceptron dimension：hypothesis是由**w**表示的，这些**w**是hypothsis的自由度，类比可以调的旋钮
* VC dimension:在二元分类时有多少自由度，衡量自由度告诉我们H到底好不好
* VC dimension物理意义：H有多少可以调的旋钮（自由度），可以估计H复杂度，以此来决定用多少资料。
![](/img/linxuant-jishi/7-6.jpg) 
#### 7.3 VC Bound REphrase
##### 7.3.1 Penalty for Model Complexity
![](/img/linxuant-jishi/7-7.jpg) 
* 通过对VC Bound进行变换，可以得到如上结果，发现一味追求小的E<sub>in</sub>（强的H）不一定得到好的E<sub>out</sub>，要同时到考虑到模型复杂付出的代价，最好的d<sub>VC</sub>在中间。
##### 7.3.2 Sample Complexity
![](/img/linxuant-jishi/7-8.jpg) 
* VC Bound对资料复杂度:理论上需要1万倍的d<sub>VC</sub>，但实际上N大约为10倍的d<sub>VC</sub>就可取到比较好的效果,可以看到VC Bound非常宽松
##### 7.3.3 Looseness of VC Bound
![](/img/linxuant-jishi/7-9.jpg) 
* VC Bound很宽松，但我们设计机器学习演算法时用到的不是它严格的部分（例如3.2提到的理论上使用1万倍的d<sub>VC</sub>），而是他表现出的哲学信息（例如3.1提到的不要一味追求最强的H）。
#### 7.4 Summary
* Learning happens if finite d<sub>VC</sub>,large N, and low E<sub>in</sub>

## Lecture 8: Noise
#### 8.1 Noise
* **x**,y都有可能有noise  
![](/img/linxuant-jishi/8-1.jpg) 
* Noise可以看做会变色的弹珠，有P概率为黄色，1-P概率为绿，但是整个罐子黄色弹珠符合某种分布，仍可用抽样方式还预测罐子中有多少黄色，即**x**来自P(**x**)，同时y来自P(y&#124;**x**)，训练的时候是如此，测试的时候还是如此，所以将VC重写后VC仍然适用。  
![](/img/linxuant-jishi/8-2.jpg) 
* Target Distribution(P(y&#124;**x**):告诉我们最好的预测(mini-target)是什么，有多少Noise  
* 对于之前讨论的determinstic target f 是Target Distribution的特殊情况：P(y&#124;**x**)=1 for y=f(**x**)  
* P(**x**)告诉我们常见、重要的点是哪些，因为P(**x**)大代表经常在E<sub>in</sub>中被sample到，同时在算E<sub>out</sub>的时候也会比较重要，所以这些点我们要尽量预测接近mini-target,这个mini-target是由Target Distribution得来的，它告诉我们最理想的mini-target是什么，所以机器学习要做到的是：在常见的点上要做的好。  
![](/img/linxuant-jishi/8-3.jpg)   
* 将f(**x**)替换为P(y|**x**)  
![](/img/linxuant-jishi/8-4.jpg)   
* 资料的性质不能推测出f的性质  
#### 8.2 Error Measure
![](/img/linxuant-jishi/8-5.jpg)   
* pointwise error measure:计算每个点的error再平均  
![](/img/linxuant-jishi/8-6.jpg)   
* 0/1 error：分类问题  
* squared error：实数问题  
![](/img/linxuant-jishi/8-7.jpg)   
* P(y/**x**)和err的衡量影响mini-target：相同P(y/**x**)时，用不同的错误衡量方法会得到不同的mini-target的结果    
* 使用0/1 error方法时，最好的mini-target=P(y/**x**)最大的  
* 使用squared error方法时，最好的mini-target是P(y/**x**)的加权平均           
![](/img/linxuant-jishi/8-8.jpg)  
* 错误衡量法法告诉A它选的g好不好                                                                                                        
#### 8.3 Choice of Error Measure
![](/img/linxuant-jishi/8-9.jpg)         
* 不同的应用需要不同的error measure,最希望的是使用者告诉我们他们最想要的错误衡量方式，但是往往使用者不能准确描述出，此时对于A设计者有两个解决方案：1.使用能说服自己的错误衡量方式(plausible) 2.使用A容易计算的错误衡量方式  
![](/img/linxuant-jishi/8-10.jpg)     
* err是真正的错误衡量方法，![](/img/linxuant-jishi/8-11.jpg)是在A中使用的错误衡量方法  
#### 8.4 Weighted Classification 
![](/img/linxuant-jishi/8-12.jpg)     
* Error Matrix:不同错误情况的权重不同   
![](/img/linxuant-jishi/8-13.jpg)     
* 将E<sup>W</sup>转换为E<sup>0/1</sup>通过copying的方式    
![](/img/linxuant-jishi/8-14.jpg)           
* Weighted Pocket Alforithm：之前学习的Pocket Algorithm可以解决E<sup>0/1</sup>问题，通过修改两个地方：1.以增大1000倍的可能性选到-1的点 2.比较新找到的E<sup>W</sup>与手里E<sup>W</sup>的大小，改造为适合不同错误权重不同的问题  
* reduction:将新问题转化到已有办法的旧问题  

## Summary : Why Can Machines Learn?
---
由于no-free-lunch理论，我们是没有办法证明g在为学习的资料上与f到底有多接近的，所以如果我们要证明学习是可能的，必须在一个假设下：Hoeffding's Intequality

![](/img/linxuant-jishi/z-1.png)    

在N较大时，部分抽样的分布可以大概率上表示整体分布。

在这个前提下，我们知到，对于一个h大概率上E<sub>in</sub>接近E<sub>out</sub>，但是我们在集和H中挑选h，这么多h，难免会有某个h运气不好中了小概率事件E<sub>in</sub>和E<sub>out</sub>差距很大，如果我们的学习算法不行选中了这个h，就使得学习失败，那么在H中出现这样bad的h(可能一个可能多个，只要有这样的h就不行)的可能性有多大呢?

![](/img/linxuant-jishi/z-2.png)    

其中M是H中h的个数，由于exp项趋于0，所以当M有限时，整体概率趋于零，也就是说，在M有限时，发生上述情况的概率趋于零，即学习是可能的。

那么当M是无穷时这个概率又会是多少呢？

虽然我们说M是无穷大，但不是所有的h都满足H的条件，例如：

![](/img/linxuant-jishi/z-3.png)    

H是二维平面上所有的直线(也就是说这个问题就是线性可分问题，所以所有候选的h构成的H是直线)，图中画叉的两幅图，他们就不满足该条件，而对于N个点，他们所能构成的最多的满足条件的组合数(真实情况下可能产生的数据，因为该问题就是线性可分问题，所以真实情况下就不能产生图中划掉的那样的数据) = 有效的直线数量 = h的数量：

![](/img/linxuant-jishi/z-4.png)    

![](/img/linxuant-jishi/z-5.png)  

我们希望M可以被有效的N所替代，所以引入了成长函数：

![](/img/linxuant-jishi/z-6.png)  

它表示N个点最多可能的组合。

不同情况(问题)下成长函数不同，有的可以直接得到，有的则不行：

![](/img/linxuant-jishi/z-7.png)  

如果没有不符合条件的组合，那么成长函数m<sub>H</sub>(n)=2<sup>n</sup>，如果我们想让上面的概率趋于零，就希望可以找到成长函数的上界，从而引入了break point:

![](/img/linxuant-jishi/z-8.png)  

它是指第一个m<sub>H</sub>(k)=2<sup>k</sup>的点k

有了break point之后，我们定义bounding function B(N,k):

![](/img/linxuant-jishi/z-9.png)  

指在break point = k时，成长函数m<sub>H</sub>(n)的最大可能的值，也就是我们要找的成长函数的上界，可以证明：

![](/img/linxuant-jishi/z-10.png)  

也就是说，B(N,k)是有上界的，并且这个上界是多项式级的，所以当存在break point时，成长函数的上界B(N,k)有上界，即当有break point时，成长函数有多项式上界(多项式上界乘以趋于0的值最终还会趋于零)。

我们得到了成长函数有上界的结论，那么我们能不能把这个成长函数直接放到上面我们算的概率式子中，就像下图所示那样？

![](/img/linxuant-jishi/z-11.png)  

其实是不能直接得到这个式子的，但是我们经过数学推导可以得到下面的式子：

![](/img/linxuant-jishi/z-12.png)    

在N很大的前提下，可以得到上式，称为VC bound，到此我们知道了当M无穷大时，如果有break point时，成长函数有多项式上界，也就是learning是成立的。  

再进一步，我们已经知道了在有break point的时候学习是可能的，那么break point的值对学习效果有什么影响吗？  

我们把最大的non-break point定义为VC Dimension, d<sub>vc</sub>:    
![](/img/linxuant-jishi/7-1.jpg)   
由于d<sub>vc</sub>是最大的非break point的点，而break point是H不能自由变化的点(不能=2<sup>n</sup>)，?所以m<sub>H</sub><=N<sup>d<sub>vc</sub></sup>,可以知道如果d<sub>vc</sub>是有限的，说明H的自由度是有限的，所以d<sub>vc</sub>衡量了H的复杂度，其实d<sub>vc</sub> = d + 1(d:perceptron的维度，也就是构成h的**w**的个数?,+1加的是w<sub>0</sub>?)  

根据以上定义，对vc bound进行变换,可以得到：  
![](/img/linxuant-jishi/7-7.jpg)     
发现对于一个特定的问题，一味追求小的E<sub>in</sub>（强的H）不一定得到好的E<sub>out</sub>，要同时到考虑到模型复杂(d<sub>vc</sub>变大，H的自由度变高模型复杂度增加)付出的代价，最好的dVC在中间。  

重写VC bound：  
![](/img/linxuant-jishi/7-8.jpg)  
可以得到对于数据量N，理论上需要1万倍的d<sub>VC</sub>，但实际上N大约为10倍的d<sub>VC</sub>就可取到比较好的效果,可以看到VC Bound非常宽松,但我们设计机器学习演算法时用到的不是它严格的部分（例如3.2提到的理论上使用1万倍的dVC），而是他表现出的哲学信息（例如3.1提到的不要一味追求最强的H）。   

所以我们可以得到结论：H中有限h时，learning成立，H中有无限h时，若成长函数存在break point，那么learning也是成立的。对于一个问题，可以有多种不同d<sub>vc</sub>(break point)的H可选，不要追求选择d<sub>vc</sub>大的，会引入模型的复杂度。  

以上我们讨论的都是没有噪声的情况，但在实际情况中，**x**,y都有可能有噪声，**x**来自P(**x**)，y来自P(y&#124;**x**)，训练和测试时都是如此，所以我们将VC进行重写之后仍然适用，也就是说在有噪声的情况下以上结论仍然成立。


