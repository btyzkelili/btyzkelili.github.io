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
## Generative Models
![](/img/lhy_ml/g-1.jpg)  
![](/img/lhy_ml/g-2.jpg)  

#### PixelRNN
![](/img/lhy_ml/g-3.jpg)  
知道前面输入的颜色是什么，就能得到输出的颜色。  
可变长度输入，可以看作是短输入补零
![](/img/lhy_ml/g-4.jpg)  
用在语音任务上，蓝色的点是声音信号，用前面的声音信号生成下一个信号，一直循环下去

#### VAE
![](/img/lhy_ml/g-5.jpg)  
auto-envoder基础上，在code上加上随机信息，再放到decoder中，新code=exp(σ)* e+m，训练要求minimize两个部分，一部分是要求输出尽可能与输入相似，一部分是minimize ∑（exp(σ)-（1+σ）+m<sup>2</sup>） 

**为什么要minimiaze ∑（exp(σ)-（1+σ）+m<sup>2</sup>）?**  
![](/img/lhy_ml/g-8.jpg)  
encoder得到m和σ，m是原始code，exp(σ)* e得到noise，m+noise得到有noise的code，由于σ可能有正有负，exp(σ)保证结果为正值，e是从normal distribution得到的，所以它的variance是固定的，乘以exp(σ)后改变了它的variance，所以exp(σ)就是noise的variance，也就是说网络自动学习variance，如果不进行任何限制的话，网络很可能会让variace为0，因为这样最容易让输出与输入相同，所以要限制variance不能太小，也就是minimize ∑（exp(σ)-（1+σ）+m<sup>2</sup>）  
![](/img/lhy_ml/g-9.jpg)  
exp(σ)是上图中蓝色的线，（1+σ）是红色的线，exp(σ)-(1+σ)是绿色的线，所以最小化exp(σ)-(1+σ)就是要求σ尽可能接近0，也就是让exp(σ)/variance尽可能接近1，保证variance不能太小

    (视频中有对公式的数学解释)

**Why VAE**  
对比pixelRNN，VAE可以控制自己画出来的图，因为code的每一维具有一定的特征/含义，可以通过控制code各维度上的值来得到不同的图，类似于将code看做拉杆  

![](/img/lhy_ml/g-7.jpg)  
对比Auto-encoder，上图左侧，如果将code表示为一维，如果靠左的code表示满月，靠右的表示半月，那他们俩中间的表示什么呢？是无法确定的，而不是介于满月与半月之间的形态，但是VAE在code基础上加了noise，要求在code前后noise范围都要尽可能像满月，所以在中间部分既要求像满月又要求像半月，也就得到满月和半月中间的形态

**conditional VAE**  
![](/img/lhy_ml/g-10.jpg)  
告诉数字的特性的分布和是什么数字，机器就可以生成和输入style相近的数字

**Problems of VAE**  
没有真正学习创造一张新图片，而是去产生一张和已知图片相似的图片，是已有图片的linear covernation

**application**  
![](/img/lhy_ml/g-6.jpg)  
用在文字任务中(writing poetry)，先选两个句子得到他们的code，将这两个code连线，在线上取点，得到一系列句子

#### GAN
![](/img/lhy_ml/g-12.jpg)  
generator不会看真正的图片

![](/img/lhy_ml/g-13.jpg)  
![](/img/lhy_ml/g-14.jpg)  
训练过程：  
首先在第一代generator输入从某个分布中得到的vector，得到一些图片，将这些图片标为0，再把真正的图片标为1，discriminator对这些数据进行学习，然后固定discriminator的参数，在generator随机输入vector，让discriminator的输出为1，generator进行学习，此时得到的图片就可以骗过第一代discriminator，然后进行下一代过程。





