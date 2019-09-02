---
layout:     post
title:      "Unsupervised Learning"
subtitle:   "Deep Generative Model "
date:       2019-09-02
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Unsupervised Learning
---  
## 1.Generative Models
![](/img/lhy_ml/g-1.jpg)  
![](/img/lhy_ml/g-2.jpg)  

## PixelIRNN
![](/img/lhy_ml/g-3.jpg)  
知道前面输入的颜色是什么，就能得到输出的颜色
![](/img/lhy_ml/g-4.jpg)  
用在语音任务上，蓝色的点是声音信号，用前面的声音信号生成下一个信号，一直循环下去

## VAE
![](/img/lhy_ml/g-5.jpg)  
auto-envoder基础上，在code上加上随机信息，再放到decoder中，但这样做的效果不太好，VAE在此基础上加了特殊处理，code=exp()*e+m，并且minimize两个部分  

VAE比起pixelIRNN是可以控制自己画出来的图，因为code的每一维代表一定的特征/含义，可以通过控制code各维度上的值来得到不同的图，类似于将code看做拉杆

![](/img/lhy_ml/g-6.jpg)  
用在文字任务中(writing poetry)，先选两个句子得到他们的code，将这两个code连线，在线上取点，得到一系列句子

