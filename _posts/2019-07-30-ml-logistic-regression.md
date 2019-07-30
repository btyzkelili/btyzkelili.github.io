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
他们的model/function set(P(C1/x))是相同的，但是根据相同的训练集挑出的f不同，w,b不同，Generative
![](/img/lhy_ml/l-11.png)  


