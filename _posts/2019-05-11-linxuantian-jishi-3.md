---
layout:     post
title:      "林轩田-机器学习基石-笔记2"
subtitle:   ""
date:       2019-07-16 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 三. How Can Machines Learn?
---
## Lecture 9: Linear Regression
---  
#### 9.1 Linear Regression Alforithm
![](/img/linxuant-jishi/9-1.jpg)   
* 与perceptron很像，perceptron=h(x)=sign(w<sup>T</sup>x)  
![](/img/linxuant-jishi/9-2.jpg)    
![](/img/linxuant-jishi/9-5.jpg)    
* 线性回归误差计算-squared error
![](/img/linxuant-jishi/9-3.jpg)    
* h(x)是一个以x为变量的方程，而E<sub>in</sub>(w)变成了一个以w为变量的方程。这样一来，我们就把“在H中寻找能使平均误差最小的方程h”这个问题，转换为“求解一个函数的最小值”的问题。X、y来源于D,是固定不变的，因此E<sub>in</sub>(w)是一个关于w的函数，使得E<sub>in</sub>(w)最小的w，就是我们要寻找的那个最优方程的参数。  
![](/img/linxuant-jishi/9-4.jpg)   
*  E<sub>in</sub>(w)图像如上图，使得E<sub>in</sub>(w)最小的w就是使得每个方向的梯度为0的w，即一阶导数为0，多元求导过程如下：  
	由于：![](/img/linxuant-jishi/9-6.jpg) 并且 ![](/img/linxuant-jishi/9-7.jpg)  
	可以得到：![](/img/linxuant-jishi/9-8.jpg)  
	令上式=0，求得w<sub>LIN</sub>：![](/img/linxuant-jishi/9-9.jpg)  
* 当X<sup>T</sup>X可逆时称为pseudo-inserse矩阵X<sup>+</sup>,大部分情况下X<sup>T</sup>X都是可逆的，因为N>>d+1(?)，不可逆时，用其他方式定义X<sup>+</sup>  
![](/img/linxuant-jishi/9-10.jpg)  
#### 9.2 Is Linear Regression a 'Learning Alforithm'?
* 用以w<sub>LIN</sub>为参数的线性方程对原始数据做预测,可以得到拟合值y^=Xw<sub>LIN</sub>=XX<sup>†</sup>y。称H=XX<sup>†</sup>为Hat Matrix，帽子矩阵，因为H为 y带上了帽子，成为y^。  
![](/img/linxuant-jishi/9-11.jpg)  
* 这张图展示的是在N维实数空间R<sup>N</sup>中，注意这里是N=数据笔数， y中包含所有真实值，y^中包含所有预测值，与之前讲的输入空间是d+1维是不一样的(?)。X中包含d+1个column(?)  
* y^=Xw<sub>LIN</sub>是X的一个线性组合,X中每个column对应R<sup>N</sup>下的一个向量，共有d+1个这样的向量，因此y^在这d+1个向量所构成的 span(平面)上。  
* 要在这个平面上找到一个向量y^使得他与真实值y之间的距离&#124;y−y^&#124;最短。不难发现当y^是y在这个平面上的投影时,即 y−y^⊥span时，&#124;y−y^&#124;最短。所以之前说过的Hat Matrix H，为y戴上帽子，所做的就是投影这个动作，寻找 span上y的投影。  
* Hy=y^，(I−H)y=y−y^。(I为单位矩阵)
* H:对称性H=H<sup>T</sup>,等幂性H<sup>2</sup>=H,半正定：所有特征值为非负数
* trace：矩阵的迹=该矩阵所有特征值的和
![](/img/linxuant-jishi/9-12.jpg)
* 假设y由f(X)∈span+noise构成的(?)。有y=f(X)+noise之前讲到H作用于某个向量，会得到该向量在span上的投影，而I−H作用于某个向量会得到那条与 span垂直的向量，在这里就是图中的y−y^即(I−H)noise=y−y^。y−y^是真实值与预测值的差，其长度就是就是所有点的平方误差之和。于是就有：  
![](/img/linxuant-jishi/9-13.jpg)   
![](/img/linxuant-jishi/9-14.jpg)  
![](/img/linxuant-jishi/9-15.jpg)  
* Ein和Eout都向σ<sup>2</sup>(noise level)收敛，并且他们之间的差异被2(d+1)N给bound住了,有点像VC bound,不过要比VC bound来的更严格一些(因为这里算出的是平均 Ein和Eout)
* 综上，由于E<sub>out</sub>（w<sub>LIN</sub>）是好的，所以学习发生了
#### 9.3 Linear Classification vs. Linear Regression
* regression的最佳w可以直接计算出来，更容易，那么可以用regression来计算classification吗？  
![](/img/linxuant-jishi/9-16.jpg)    
![](/img/linxuant-jishi/9-17.jpg)  
![](/img/linxuant-jishi/9-18.jpg)    
* 由于err<sub>0/1</sub>总小于err<sub>sqr</sub>，所以regression E<sub>in</sub>(w)可以作为classification E<sub>out</sub>(w)的一个上界，所以可以用regression代替classification,效果可能还可以，可以作为基础款分类。
* 也可以用regression直接得到w作为PLA/pocket的初始w，从一个接近最好结果的w开始算法可能会加快计算过程。

## Lecture 10: Logistic Regression
---
#### 10.1 Logistic Regression
![](/img/linxuant-jishi/10-4.PNG) 
![](/img/linxuant-jishi/10-3.PNG)  
* logictic regression可以看做是soft的二元分类，他要得到的结果不再是0或1，而是一个0~1的值(概率)

![](/img/linxuant-jishi/10-5.PNG)  
* 理想情况下，我们希望得到(x,P(+1&#124;x))样子的数据，就可以像之前一样做，但实际情况下我们只有y=0/1的数据(就像我们需要告知病人他得病的概率，但是没有人知道这个概率是多少，我们只能知道他最有到底有没有得病)，这个0/1的数据可以看成是理想情况下数据的有噪声版本。

![](/img/linxuant-jishi/10-6.PNG)  
* 我们先根据w和x计算s，再通过logistic function将s转换到01之间，就可以得到logistic hypothesis

![](/img/linxuant-jishi/10-1.PNG)  
* logistic function图像如上，它是一个smooth、monotonic(单调)、sigmoid(s型的)函数

![](/img/linxuant-jishi/10-2.PNG)  
* 那么我们应该怎样定义logistic regression 的 E<sub>in</sub>呢？

#### 10.2 Logistic Regression Error
![](/img/linxuant-jishi/10-7.PNG)  
* 在f情况下(真实情况下的概率)，产生资料D的概率为上图的左边，如果我们假设h非常接近f，那么h也产生资料D的可能性如上图右边(将f替换成h），如果h非常接近f，那么他们产生资料D的概率也很接近，资料D是由f产生的，所以好的h(接近f的h)产生D的概率会很高，就是说，对于很多病人(x1,x2...)他们真实情况下得病的概率(f)为(p1,p2...)，所以会产生有p(x1)p1p(x2)p(1-2)...可能性产生资料((x1,1),(x2,0)...)...，如果有一个h，在它的是否生病的概率下，产生D的概率非常高，说明h和f很接近

![](/img/linxuant-jishi/10-8.PNG)
* 要求在h在的可能性最大值，就是求上图中的min(化简过程略，较简单)
* cross-entropy error: err(**w**,**x**,y)=ln(1+exp(-y**wx**))

![](/img/linxuant-jishi/10-9.PNG)
* 找到E<sub>in</sub>之后，怎么找到w使得E<sub>in</sub>最小？

#### 10.3 Gradient of Logistic Regression Error
![](/img/linxuant-jishi/10-10.PNG)
* E<sub>in</sub>的图像如上图左，对其求梯度(求对**w**的偏微分)，最小的E<sub>in</sub>就是使其梯度为0(神经网络是求解试得梯度为0的w的一种方法)
* 梯度的反方向是下降最快的方向

#### 10.4 Gradient Descent
![](/img/linxuant-jishi/10-11.PNG)
![](/img/linxuant-jishi/10-12.PNG)
* 怎么求使得梯度为0的w？由于难以像线性一样直接得到w，所以可以用不断更新w的方法(像PLA)：梯度下降
* 梯度下降：对w往梯度的反方向走

![](/img/linxuant-jishi/10-13.PNG)
![](/img/linxuant-jishi/10-14.PNG)
* 如何确定yita呢？应该在坡度大的地方走的步子大一点，坡度小的地方走的步子小一点，所以yita和&#124;&#124;E<sub>in</sub>(w)&#124;&#124;成正比
* 新的yita叫做学习率

## Lecture 11: linear models for classification
---
#### 11.1 Linear Models for Binary Classification 

![](/img/linxuant-jishi/11-1.PNG)    
* linear classification是NP问题，所以我们需要找到一种容易解决他的方法，就是利用linear regression和logistics regression作为其上限来求解。

![](/img/linxuant-jishi/11-2.PNG)   
* 将三种err变换为ys形式
* ys物理意义: y代表正确的，s是打分，所以ys代表correctness score

![](/img/linxuant-jishi/11-3.PNG)   
* 0/1 err图像如蓝线所示，sq r err如红线所示，scaled ce err 如黑线所示(scaled是ce err的log<sub>2</sub>形式，为了让黑线与其他两线相交与一点，方便分析)
* 从图上可以看出，较小的ys下，sqr err和0/1 err 都认为是不太好的情况(err 值大)，而d当ys较大时，0/1 err认为较好的情况sqr认为较差，使得sqr err不能代表0/1,对于scaled ce err，它可以较好的代表0/1 err

![](/img/linxuant-jishi/11-4.PNG)   
* 理论推导如上，也就是说，如果我们把logistic/linear regression做好，就也把linear classification做好了，只不过logistic regression的限制更宽松

![](/img/linxuant-jishi/11-5.PNG)   
* 用logistic/linear regression在资料上学习得到**w**，再得到g(x)=sign(**wx**)
* 如果使用linear regression:optimization最简单，有直接公式，但是限制宽松，可能与0/1err有较大差距
* 如果使用logistic regression:由于它是smooth、convex所以可以用梯度下降，optimization也较为简单，但是也只是一个上限
* 如果使用PLA，只有在linear separable时效果比较好
* 所以建议，logistic regression去找到PLA/pocket/logistic regression的w0；更常用logistic regression而不是pocket(因为每轮的工作差不多，但是optimization更简单)

#### 11.2 Stochastic Grad.Descent

![](/img/linxuant-jishi/11-6.PNG)   
* PLA每次只需要找到一个不正确的点进行更新O(1)，而logistic regression需要所有点一起去计算梯度，再找梯度下降的方向O(n)，时间上和pocket一样(pocket是计算所有点找比自己手里好的)

![](/img/linxuant-jishi/11-7.PNG)   
* 我们希望logistic的速度可以和PLA一样快，采取的方法是，每次不计算所有点的梯度，而是只随机抽取一个点来计算，理论依据是只抽取一部分点，也可以基本代表整体的分布，只是我们做的更加极端，只抽取一个点
* 随机梯度下降SGD：优点是简单且耗费低，坏处是不稳定，很难决定什么时候停，一般是相信跑够久就停，经验上yita=0.1

#### 11.3 Multiclass via Logistic Regression
![](/img/linxuant-jishi/11-8.PNG)   
* 处理多分类问题，可以训练多个二元分类器，每个分类器针对起皱一个类别判断是或否。
* 缺点是会出现多个分类器抢一个类别，或者没有分类器认为是自己类别的点。

![](/img/linxuant-jishi/11-9.PNG)   
* 可以用更soft的方法，每个分类器是logistic regression，判断是自己类别的概率:
* One-Versus-All(OVA) Decomposition: 对每个类别跑一个logistive regression，跑完后选择这些h个里给出分数最高的。优点是有效，坏处是当数据不平均分布(unbalance)的话，全部预测是错误是可能就会有很高的正确率，会让表现变差。
* 对该办法的延申：multinomial('coupled')logistic regression

#### 11.4 Multiclass via Binary Classification
![](/img/linxuant-jishi/11-10.PNG)   
* 每次选两个类别做二元分类，最后根据分类器的投票决定到底是哪个类别

![](/img/linxuant-jishi/11-11.PNG)   
* One-versus-ine(OVO) Decomposition

## Lecture 12: Nonlinear Transformation
---
#### 12.1 Quadratic Hypotheses
![](/img/linxuant-jishi/12-1.PNG)     

* 之前讲的都是线性情况：s=**w<sup>T</sup>x**，每个w和x的一次方相乘后再加起来，得到的是一个将点划分成两半的直线，现在我们的点不在能用一条直线划分开，需要一个圈，所以我们进行特征转换feature transform，将x<sub>1</sub><sup>2</sup>对应z<sub>1</sub>，x<sub>2</sub><sup>2</sup>对应z<sub>2</sub>，这样在x空间的圈即可对应z空间的直线.

![](/img/linxuant-jishi/12-1.PNG)     

* 更进一步，z空间的线对应x空间特殊的曲线(圆、椭圆、双曲线等)，反之亦然。

![](/img/linxuant-jishi/12-1.PNG)     

* 将z空间进一步扩大，涵盖所有x的一次二次方，即可表示所有可能的曲线，所以只要在z空间里找到一条好的直线，就可以在x空间找到好的曲线。

#### 12.2 Nonlinear Transform

![](/img/linxuant-jishi/12-4.PNG)  
![](/img/linxuant-jishi/12-5.PNG)      

* 首先，将x空间的点转换到z空间，然后在z空间好的直线，然后用x空间的点找到其在z空间的对应点，看看对应点在z空间直线的哪一边，来决定x空间的点是o还是×(而不是将z空间的直线转换为曲线，可能并不存在这样的转换)，这样就可以轻松完成suqduatic PLA\quadratic regression\cubic regression\polynomial regression...

![](/img/linxuant-jishi/12-6.PNG)     

* 关于特征转换，在之前讲过如何分辨手写数字是否为1，可以将图片特征转换为对称性等其他特征，来完成对判断，即把raw转换为concrete。

#### 12.3 Price of Nonlinear Transform

![](/img/linxuant-jishi/12-7.PNG)     

* 进行特征转换之后，对需要存储大规模的向量，计算时也更加困难

![](/img/linxuant-jishi/12-8.PNG)     

* E<sub>in</sub>非常小的时候难以让E<sub>out</sub>与E<sub>in</sub>足够相似，而E<sub>out</sub>与E<sub>in</sub>足够相似时，E<sub>in</sub>又难以足够小

![](/img/linxuant-jishi/12-9.PNG)     

* 不要把自己视觉化或者大脑里得到的放到机器学习中(不要偷看数据)，不然会对自己的算法过于乐观，虽然在自己的推理下vc小，那是因为没有计算大脑里的vc。

#### 12.4 Structured Hypothesis Sets

![](/img/linxuant-jishi/12-10.PNG)     

* H可以包含其他H，叫做H的structure

![](/img/linxuant-jishi/12-11.PNG)    

* H越大，vc越大，E<sub>in</sub>越小，但我们的目的并不是找到最小的E<sub>in</sub>，而是小的E<sub>out</sub>

![](/img/linxuant-jishi/12-12.PNG)     

* 先从线性模型开始，简单、有效、安全、而且一般表现都不错

## Summary: How Can Machines Learn?
在这一章节中，我们介绍了几种学习算法：linear regression、logistic regression、线性分类(二分类、多分类)、非线性转换

对于线性回归，我们可以直接用公式计算出使E<sub>in</sub>最小的**w**：
![](/img/linxuant-jishi/9-10.jpg)  
![](/img/linxuant-jishi/9-9.jpg)  

对于logistic regression：
是一种soft分类，利用sigmiod函数将输出值映射到[0,1]之间,用cross-entropy error衡量错误(使产生真实资料的可能性越大越好)：  
![](/img/linxuant-jishi/10-8.PNG)  
以此得到E<sub>in</sub>:
![](/img/linxuant-jishi/10-9.PNG)  
通过梯度下降来得到E<sub>in</sub>min,梯度下降时要注意学习率的设置，一般可取0.1

对于线性二分类，这是一个NP问题，所以我们通过线性回归和ligistic回归来求其上界解决，一般建议logistic regression找PLA/pocket/logistic regression的w0

对于先行多分类，可通过logistic regression解决:OVA,也可通过binary classification解决:OVO

对于非线性转换：可通过特征转换将**x**映射到线性空间，但是特征转换要付出计算和存储空间上的代价，所以建议优先从线性模型开始，一般变现都不错。








