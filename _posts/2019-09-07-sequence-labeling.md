---
layout:     post
title:      "Structure Learning"
subtitle:   "Sequence Labeling"
date:       2019-09-07
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - SVM
---  
## Sequence Labeling
![](/img/lhy_ml/seq-1.jpg)  
Sequence Label是从sequence到sequence的任务，并且输入输出长度相同，我们以POS tagging为例

## POS tagging
![](/img/lhy_ml/seq-2.jpg)  
已知一句话，得到句子中每个词的词性  
![](/img/lhy_ml/seq-3.jpg)  
以上面过程研究POS tagging问题  

#### HMM
![](/img/lhy_ml/seq-4.jpg)  
整体思路：我们说出一句话，首先要想好这句话每个词的词性组合，然后给对应的词性填上具体单词，以下是一个具体的计算例子：  
![](/img/lhy_ml/seq-5.jpg)  ![](/img/lhy_ml/seq-6.jpg)  ![](/img/lhy_ml/seq-6.jpg)  
一般化过程：  
![](/img/lhy_ml/seq-8.jpg)  
![](/img/lhy_ml/seq-9.jpg)  ![](/img/lhy_ml/seq-10.jpg)  
如何得到P(V/PV)、P(saw/V)呢？首先需要语言学家对数据中每个词的词性进行标注，然后根据上式计算(统计出现次数)

那么如何用HMM解决POS tagging问题呢？
![](/img/lhy_ml/seq-11.jpg)  
也就是找到让P(x,y)最大的y
![](/img/lhy_ml/seq-12.jpg)  
找最大的y有算法viterbi

**Summery HMM**  
![](/img/lhy_ml/seq-13.jpg)  
HMM是structure learning的一种方法，所以要回答structure learning的三个问题
![](/img/lhy_ml/seq-14.jpg)  
HMM会脑补数据，有可能出现认为没有出现的数据的概率比出现的数据概率高，这是因为它的transition probability和emission probability
是分开model的，他假设这两个几率是independent，这件事有好有坏，在训练数据很少的时候，HMM表现更好，可以用更复杂的模型解决这个问题(CRF)

#### CRF
CRF实质上和HMM是一样的，视频课程有证明  
![](/img/lhy_ml/seq-15.jpg)  
CRF模型是P(x,y)正比于exp(w·Φ(x,y))，其中Φ由两部分组成：
![](/img/lhy_ml/seq-16.jpg)  
第一部分：所有词性和所有词组成的pair，给一个pair，看(x,y)中出现该pair的次数，维度是S* L
![](/img/lhy_ml/seq-17.jpg)  
第二部分：连续出现的两个词性的pair，给一个paire，看(x,y)出现该pair的次数，维度是S* S+2S
![](/img/lhy_ml/seq-18.jpg)  
也可以自己定

**training**  
![](/img/lhy_ml/seq-19.jpg)  
CRF希望让training data中有的(x,y)pair大，没看到的小，用gradient ascent来进行更新：  
![](/img/lhy_ml/seq-20.jpg)  
![](/img/lhy_ml/seq-21.jpg)  
![](/img/lhy_ml/seq-22.jpg)  
![](/img/lhy_ml/seq-23.jpg)  

**testing**  
![](/img/lhy_ml/seq-24.jpg)  

**CRF vs HMM**  
![](/img/lhy_ml/seq-25.jpg)  
CRF会减少没有出现的数据的概率，CRF更有可能得到正确的结果

**CRF summary**  
![](/img/lhy_ml/seq-26.jpg)  
CRF是structure learning的一种方法，所以要回答structure learning的三个问题

#### Structured Perceptron
![](/img/lhy_ml/seq-27.jpg)  
![](/img/lhy_ml/seq-28.jpg)  
Structure只减去最大概率的Φ-->heard，而CRF会减去所有Φ的weighted sum-->soft，但是CRF要求∑有事会比较困难，如果难以解，建议用
Structure Perceptron

#### Structure SVM
![](/img/lhy_ml/seq-29.jpg)  
![](/img/lhy_ml/seq-30.jpg)  
重要的是设计error function Δy，能够计算出在有Δy的情况下得到与x最匹配的y

![](/img/lhy_ml/seq-31.jpg)  

#### How about RNN?
![](/img/lhy_ml/seq-32.jpg)  
1. 单向RNN在输出一个结果时只看了这个位置之前的内容，不会看完所有sequence，双向RNN不知道会有怎样的优劣  
2. HMM等可以明确考虑output的label与label之间的关系，在穷举所有sequence的时候，只穷举符合规定条件的sequence，
类似中文是一个声母后面加一个韵母，RNN需要自己学习到这些条件  
3. RNN的cost和error不一定有关联，RNN可以deep，因为deep太强了所以还是RNN胜利

**Integrated together**
![](/img/lhy_ml/seq-33.jpg)  
![](/img/lhy_ml/seq-34.jpg)  
因为输入x是固定的，所以红线划掉该项
![](/img/lhy_ml/seq-35.jpg)  
x来自于RNN

## Concluding
![](/img/lhy_ml/seq-36.jpg)  
