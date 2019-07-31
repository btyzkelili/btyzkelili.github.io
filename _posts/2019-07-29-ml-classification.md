---
layout:     post
title:      "Machine Learning"
subtitle:   "Classification"
date:       2019-07-29
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Machine Learning
---  
## 1. Clssificatin as Regression?
![](/img/lhy_ml/c-1.png)  
Regression对于model好坏的定义不适用于classification，如右图，存在>>1的点时，regression更倾向于向右偏来减小平方和err  

## 2.Probabilistic Generative Model
![](/img/lhy_ml/c-2.png)  
我们要想知道现有的x(一笔资料)时类别一还是类别二，可以计算P(C1/x)，要计算这个概率，需要通过training data得到P(C1)=C1数据个数/总数据个数、
P(C2)、P(x/C1)、P(x/C2)  

P(x)可以知道任意x产生的概率，所以叫做Generative Model(生成模型)  

怎么计算一个在训练集中没有的x的P(x/C1)呢？P(C1)P(C2)好计算，那P(x/C1)、P(x/C2)如何得到？

![](/img/lhy_ml/c-3.png)  ![](/img/lhy_ml/c-4.png)  
我们假设每一个类别的x的产生来自于一个高斯分布，高斯分布有两个参数∑(也就是σ<sup>2</sup>)和μ，任何一个高斯分布都可以sample出这个类别的training data，
但sample出的概率L(μ,∑)不同，假设每笔资料之间独立分布，L(μ,∑)=f(x1)f(x2)...f(xn)(图中n=79笔该类别资料)，找到使L(μ,∑)最大的μ,∑的高斯分布f的结果作为产生x的概率

为什么要用高斯分布？
![](/img/lhy_ml/c-10.png)  
可以使用任何符合feature特点的其他分布方式

![](/img/lhy_ml/c-5.png) 
当x有k个feature时，类别n的μ<sup>n</sup>(class n的μ)：k-dim vector，∑<sup>n</sup>：k * k matrices：

![](/img/lhy_ml/c-6.png) 
根据以上方法求得P(x/C1)、P(x/C2)、P(C1)、P(C2)，可以计算P(C1/x)，如果P>0.5则认为是class1

* 模型改进：  
![](/img/lhy_ml/c-7.png) 
![](/img/lhy_ml/c-8.png) 
用上面的方法做的效果可能不是很好，一般的做法是让不同类别共享∑，来减少参数数量，并让L(μ<sup>1</sup>,μ<sup>2</sup>,∑)尽可能大(之前是让每一个类别的L(μ,∑)尽可能大，
现在是让所有类别的L(μ<sup>1</sup>,μ<sup>2</sup>,∑)尽可能大)，修改L后，P(C1/x)=0从曲线变成了直线，为什么会变为直线(linear model)？  
![](/img/lhy_ml/c-11.png)  
![](/img/lhy_ml/c-12.png)  
将P(C1/x)变形，其中z可以化简为上图式子，我们假设∑都相等，可以得到z=**w**<sup>T</sup>x+b，所以P(C1/x)=σ(**w**<sup>T</sup>x+b)，也就是一个linear model，
既然如此，我们可以直接找**w**和b，而不用先找N1、N2、μ<sup>1</sup>、μ<sup>2</sup>、∑再计算**w**、b

## 3. Probabilistic Generative Model 步骤：  
![](/img/lhy_ml/c-9.png) 
1. 找到model:P(c1/x)
2. model好坏的评价函数L(μ<sup>1</sup>,μ<sup>2</sup>,∑)
3. 挑选最好的model(可以求微分解)

## 4. Probabilistic_Generative.py
```python3
import pandas as pd
import numpy as np
from random import shuffle
from numpy.linalg import inv
from math import floor, log
import os
import argparse

output_dir = "output/"

def dataProcess_X(rawData):

    #sex 只有两个属性 先drop之后处理
    if "income" in rawData.columns:
        Data = rawData.drop(["sex", 'income'], axis=1)
    else:
        Data = rawData.drop(["sex"], axis=1)
    listObjectColumn = [col for col in Data.columns if Data[col].dtypes == "object"] #读取非数字的column
    listNonObjedtColumn = [x for x in list(Data) if x not in listObjectColumn] #数字的column

    ObjectData = Data[listObjectColumn]
    NonObjectData = Data[listNonObjedtColumn]
    #insert set into nonobject data with male = 0 and female = 1
    NonObjectData.insert(0 ,"sex", (rawData["sex"] == " Female").astype(np.int))
    #set every element in object rows as an attribute
    ObjectData = pd.get_dummies(ObjectData)

    Data = pd.concat([NonObjectData, ObjectData], axis=1)
    Data_x = Data.astype("int64")
    # Data_y = (rawData["income"] == " <=50K").astype(np.int)

    #normalize
    Data_x = (Data_x - Data_x.mean()) / Data_x.std()

    return Data_x

def dataProcess_Y(rawData):
    df_y = rawData['income']
    Data_y = pd.DataFrame((df_y==' >50K').astype("int64"), columns=["income"])
    return Data_y


def sigmoid(z):
    res = 1 / (1.0 + np.exp(-z))
    return np.clip(res, 1e-8, (1-(1e-8)))

def _shuffle(X, Y):                                 #X and Y are np.array
    randomize = np.arange(X.shape[0])
    np.random.shuffle(randomize)
    return (X[randomize], Y[randomize])

def split_valid_set(X, Y, percentage):
    all_size = X.shape[0]
    valid_size = int(floor(all_size * percentage))

    X, Y = _shuffle(X, Y)
    X_valid, Y_valid = X[ : valid_size], Y[ : valid_size]
    X_train, Y_train = X[valid_size:], Y[valid_size:]

    return X_train, Y_train, X_valid, Y_valid

def valid(X, Y, mu1, mu2, shared_sigma, N1, N2):
    sigma_inv = inv(shared_sigma)
    # 3.上面的图中有w和b的公式
    w = np.dot((mu1-mu2), sigma_inv)
    X_t = X.T
    b = (-0.5) * np.dot(np.dot(mu1.T, sigma_inv), mu1) + (0.5) * np.dot(np.dot(mu2.T, sigma_inv), mu2) + np.log(float(N1)/N2)
    a = np.dot(w,X_t) + b
    y = sigmoid(a)
    # around四舍五入
    y_ = np.around(y)
    result = (np.squeeze(Y) == y_)
    print('Valid acc = %f' % (float(result.sum()) / result.shape[0]))
    return

# 根据训练集计算u1 u2 sigma N1 N2
def train(X_train, Y_train):
    # vaild_set_percetange = 0.1
    # X_train, Y_train, X_valid, Y_valid = split_valid_set(X, Y, vaild_set_percetange)

    #Gussian distribution parameters
    train_data_size = X_train.shape[0]

    cnt1 = 0
    cnt2 = 0

    mu1 = np.zeros((106,))
    mu2 = np.zeros((106,))
    for i in range(train_data_size):
        if Y_train[i] == 1:     # >50k
            mu1 += X_train[i]
            cnt1 += 1
        else:
            mu2 += X_train[i]
            cnt2 += 1
    mu1 /= cnt1
    mu2 /= cnt2

    sigma1 = np.zeros((106, 106))
    sigma2 = np.zeros((106, 106))
    for i in range(train_data_size):
        if Y_train[i] == 1:
            sigma1 += np.dot(np.transpose([X_train[i] - mu1]), [X_train[i] - mu1])
        else:
            sigma2 += np.dot(np.transpose([X_train[i] - mu2]), [X_train[i] - mu2])

    sigma1 /= cnt1
    sigma2 /= cnt2
    shared_sigma = (float(cnt1) / train_data_size) * sigma1 + (float(cnt2) / train_data_size) * sigma2

    N1 = cnt1
    N2 = cnt2

    return mu1, mu2, shared_sigma, N1, N2


if __name__ == "__main__":
    trainData = pd.read_csv("data/train.csv")
    testData = pd.read_csv("data/test.csv")
    ans = pd.read_csv("data/correct_answer.csv")

# here is one more attribute in trainData
    x_train = dataProcess_X(trainData).drop(['native_country_ Holand-Netherlands'], axis=1).values
    x_test = dataProcess_X(testData).values
    y_train = dataProcess_Y(trainData).values
    y_ans = ans['label'].values

    vaild_set_percetange = 0.1
    X_train, Y_train, X_valid, Y_valid = split_valid_set(x_train, y_train, vaild_set_percetange)
    mu1, mu2, shared_sigma, N1, N2 = train(X_train, Y_train)
    valid(X_valid, Y_valid, mu1, mu2, shared_sigma, N1, N2)

    mu1, mu2, shared_sigma, N1, N2 = train(x_train, y_train)
    sigma_inv = inv(shared_sigma)
    w = np.dot((mu1 - mu2), sigma_inv)
    X_t = x_test.T
    b = (-0.5) * np.dot(np.dot(mu1.T, sigma_inv), mu1) + (0.5) * np.dot(np.dot(mu2.T, sigma_inv), mu2) + np.log(
        float(N1) / N2)
    a = np.dot(w, X_t) + b
    y = sigmoid(a)
    y_ = np.around(y).astype(np.int)
    df = pd.DataFrame({"id" : np.arange(1,16282), "label": y_})
    result = (np.squeeze(y_ans) == y_)
    print('Test acc = %f' % (float(result.sum()) / result.shape[0]))
    df = pd.DataFrame({"id": np.arange(1, 16282), "label": y_})
    if not os.path.exists(output_dir):
        os.mkdir(output_dir)
    df.to_csv(os.path.join(output_dir+'gd_output.csv'), sep='\t', index=False)

```

