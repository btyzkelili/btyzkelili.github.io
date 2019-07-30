---
layout:     post
title:      "Machine Learning"
subtitle:   "Logistic Regression"
date:       2019-07-30
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Machine Learning
---  
## 1. Logistic Regression
![](/img/lhy_ml/l-1.png)  ![](/img/lhy_ml/l-2.png)  
第一步，找function set  

![](/img/lhy_ml/l-3.png)  ![](/img/lhy_ml/l-4.png)  ![](/img/lhy_ml/l-5.png)  
第二步，评价f的好坏  
cross entropy H(p,q)=-∑p(x)ln(q(x)): 衡量两个分布有多接近，越小越接近，=0是表示分布相同。在这里是把f的output和target的output看成分布，
希望他们越接近越好

![](/img/lhy_ml/l-6.png)  
第三步，找最好的f  
对-lnL(w,b)求微分，使用梯度下降更新参数，微分结果表示输出结果值和目标值相差越大更新越大

#### 1.2 square error?
![](/img/lhy_ml/l-7.png)  ![](/img/lhy_ml/l-8.png)  
f输出只有0/1，当f输出y=0，实际target输出为1，距离target较远时，square error的微分值为0，不会更新参数。从上图可以看到，在远离最低点的位置上，
square error的微分仍然很小，更新速度慢

## 2. Logistic and Linear Regression
![](/img/lhy_ml/l-9.png)  
他们的计算出的梯度是相同的，但是logistic Regression的输出只能在0~1，y只能是0/1

## 3. Discriminative and Generative
![](/img/lhy_ml/l-10.png)  
他们的model/function set(P(C1/x))是相同的，但是根据相同的训练集挑出的f不同
![](/img/lhy_ml/l-11.png)  
对于上面的例子，使用Naive Bayes(features之间独立)，得到[1,1]是类型2，而非类型1，这是因为Generative模型会脑补，即使训练集里class2中没有[1,1]，模型也不会认为class2的[1,1]概率为0  

![](/img/lhy_ml/l-12.png)  
通常认为discriminative更好一些，但是在训练数据较少，有noise时，generative会更有效

## 4. Multi-class Classification
![](/img/lhy_ml/l-13.png)  ![](/img/lhy_ml/l-14.png)  
将二分类中sigmoid换成了sofmax

## 5. Limitation of Logistic Regression
![](/img/lhy_ml/l-15.png)  
logistic regression是一个线性模型，无法分开非线性数据

![](/img/lhy_ml/l-16.png)  
fearture transformation：可以对非线性数据进行特征转换，变为线性数据，再使用logistic regression

![](/img/lhy_ml/l-17.png)  
特征转换过程可以看作一次logistic regression，多个logistic regression串接完成对非线性数据的分类，多个logistic regression的参数可以同时训练，也就是deep learning












