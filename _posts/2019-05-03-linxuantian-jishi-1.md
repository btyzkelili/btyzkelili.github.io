---
layout:     post
title:      "林轩田-机器学习基石-Lecture1"
subtitle:   ""
date:       2019-05-04 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 一. When Can Machines Learn?
## Lecture 1: The Learning Problem
---  
### 1. What is machine learning?  
![](/img/linxuant-jishi/1.jpg)  
* 机器学习处理数据提高某方面的表现  

### 2. When to use machine learning?  
![](/img/linxuant-jishi/2.jpg)  
 1. 存在某些可以学习（可以预测）的潜藏模式，某种表现可以增进  
 2. 不知道如何定义 eg.无法定义什么是树 
 3. 模式有data     
* Example:   
![](/img/linxuant-jishi/3.jpg)  
![](/img/linxuant-jishi/4.jpg)  

### 3. Components of Learning  
![](/img/linxuant-jishi/6.jpg)  
1. 输入input：**x**=(x<sub>1</sub>,x<sub>2</sub>,...,x<sub>b</sub>),每个x代表一个特征的值，一个特征可以用多维向量表示  
2. 输出output: y(label)  
3. 目标函数f：未知(需要学习的模式，知道就不用使用机器学习)  
4. 数据(**x**,y)  
5. 假说函数g:尽可能与f相似  

### 4. The Learning Model  
![](/img/linxuant-jishi/5.jpg)  
* 机器学习演算法A:有两个输入：数据和H(hypothsis set),任务是从很多可能的公式h(**x**)组成的H(hypothesis set)中选一个它认为最接近f的g  
* 机器学习模型：A and H
* 机器学习进一步定义：使用数据计算尽可能接近f的g  
* Example:   
![](/img/linxuant-jishi/7.jpg)  
![](/img/linxuant-jishi/8.jpg)  

### 5. Machine and other disciplines  
#### 5.1 Machine Learning and Data Mining  
![](/img/linxuant-jishi/11.jpg)  
* 机器学习和数据挖掘在实际中很难区分，但是并不是一样的  
  
#### 5.2 Machine Learning and Artificial Intelligence  
![](/img/linxuant-jishi/10.jpg)  
* 机器学习是实现人工智能的一个方法  
  
#### 5.3 Machine Learning and Statistics  
![](/img/linxuant-jishi/9.jpg)  
* 统计方法有很多机器学习可以借鉴的方法  
