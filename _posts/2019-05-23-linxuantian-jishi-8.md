---
layout:     post
title:      "林轩田-机器学习基石-Lecture8"
subtitle:   ""
date:       2019-05-23
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 二. Why Can Machines Learn?
## Lecture 8: Noise
## 1.Noise
* **x**,y都有可能有noise  
![](/img/linxuant-jishi/8-1.jpg) 
* Noise可以看做会变色的弹珠，有P概率为黄色，1-P概率为绿，但是整个罐子黄色弹珠符合某种分布，仍可用抽样方式还预测罐子中有多少黄色，即**x**来自P(**x**)，同时y来自P(y&#124;**x**)，训练的时候是如此，测试的时候还是如此，所以将VC重写后VC仍然适用。  
![](/img/linxuant-jishi/8-2.jpg) 
* Target Distribution(P(y&#124;**x**):告诉我们最好的预测(mini-target)是什么，有多少Noise  
* 对于之前讨论的determinstic target f 是Target Distribution的特殊情况：P(y|**x**)=1 for y=f(**x**)  
* P(**x**)告诉我们常见、重要的点是哪些，因为P(**x**)大代表经常在E<sub>in</sub>中被sample到，同时在算E<sub>out</sub>的时候也会比较重要，所以这些点我们要尽量预测接近mini-target,这个mini-target是由Target Distribution得来的，它告诉我们最理想的mini-target是什么，所以机器学习要做到的是：在常见的点上要做的好。  
![](/img/linxuant-jishi/8-3.jpg)   
* 将f(**x**)替换为P(y|**x**)  
![](/img/linxuant-jishi/8-4.jpg)   
* 资料的性质不能推测出f的性质  
## 2.Error Measure
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
## 3.Choice of Error Measure
![](/img/linxuant-jishi/8-9.jpg)         
* 不同的应用需要不同的error measure,最希望的是使用者告诉我们他们最想要的错误衡量方式，但是往往使用者不能准确描述出，此时对于A设计者有两个解决方案：1.使用能说服自己的错误衡量方式(plausible) 2.使用A容易计算的错误衡量方式  
![](/img/linxuant-jishi/8-10.jpg)     
* err是真正的错误衡量方法，![](/img/linxuant-jishi/8-11.jpg)是在A中使用的错误衡量方法  
## 4.Weighted Classification 
![](/img/linxuant-jishi/8-12.jpg)     
* Error Matrix:不同错误情况的权重不同   
![](/img/linxuant-jishi/8-13.jpg)     
* 将E<sup>W</sup>转换为E<sup>0/1</sup>通过copying的方式    
![](/img/linxuant-jishi/8-14.jpg)           
* Weighted Pocket Alforithm：之前学习的Pocket Algorithm可以解决E<sup>0/1</sup>问题，通过修改两个地方：1.以增大1000倍的可能性选到-1的点 2.比较新找到的E<sup>W</sup>与手里E<sup>W</sup>的大小，改造为适合不同错误权重不同的问题  
* reduction:将新问题转化到已有办法的旧问题  
