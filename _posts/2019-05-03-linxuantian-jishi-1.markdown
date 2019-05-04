---
layout:     post
title:      "林轩田-机器学习基石-笔记1"
subtitle:   ""
date:       2019-05-04 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
#When Can Machines Learn?#
##Lecture 1: The Learning Problem##
###What is machine learning?  
![](https://i.imgur.com/spYNGz8.jpg)  
机器学习处理数据提高某方面的表现  

###When to use machine learning?  
![](https://i.imgur.com/1JVHcG6.jpg)  
 1. 存在某些可以学习（可以预测）的潜藏模式，某种表现可以增进  
 2. 不知道如何定义 eg.无法定义什么是树 
 3. 模式有data   
eg.   
![](https://i.imgur.com/gFZrCBX.jpg)  
![](https://i.imgur.com/GbtxMO4.jpg)  

###Components of Learning  
![](https://i.imgur.com/N60ZXtz.jpg)  
1. 输入input：x  
2. 输出output: y  
3. 目标函数f：未知(需要学习的模式，知道就不用使用机器学习)  
4. 数据(x,y)  
5. 假说函数g:尽可能与f相似  

###The Learning Model  
![](https://i.imgur.com/lpkqAyH.jpg)  
* 机器学习演算法A:有两个输入：数据和H(hypothsis set),任务是从很多可能的公式h组成的H(hypothesis set)中选一个它认为最接近f的g  
* 机器学习模型：A and H
* 机器学习进一步定义：使用数据计算尽可能接近f的g  
eg.   
![](https://i.imgur.com/dpu4Ywd.jpg)  
![](https://i.imgur.com/WH8Lia3.jpg)  

###Machine Learning and Data Mining  
![](https://i.imgur.com/BDOAF25.jpg)  
机器学习和数据挖掘在实际中很难区分，但是并不是一样的  
  
###Machine Learning and Artificial Intelligence  
![](https://i.imgur.com/bvTGqOb.jpg)  
机器学习是实现人工智能的一个方法  
  
###Machine Learning and Statistics  
![](https://i.imgur.com/kkWLWMv.jpg)  
统计方法有很多机器学习可以借鉴的方法  
