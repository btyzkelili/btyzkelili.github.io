---
layout:     post
title:      "Machine Learning"
subtitle:   "Introduction of Machine Learning and Regression"
date:       2019-07-25
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Machine Learning
---  
## 0. Machine Learning
![](/img/lhy_ml/1.png)  
在有机器学习之前，实现人工智能的方式：hand-crafied rules，成千上万的if，永远无法超越创造者，
并且需要耗费大量的人力。

那什么是Machine Learning?
**Machine Learning≈Looking for a function**
![](/img/lhy_ml/2.png)  
1. 找一个f的集合，也就是模型
2. 让机器能够根据数据衡量一个f的好坏，通过loss function：输入f输出它的好坏，L(f)=L(w,b)
3. 挑选出最好的f
![](/img/lhy_ml/3.png)  
蓝色部分是scenaio(方案)，是由问题决定的，能用有监督就不应该用强化学习，红色部分是在方案下所选择的task，
绿色部分是每种task下可用的解决方法

## 1. Regression
#### 1.1 Regression Example
提出一个回归问题：  
![](/img/lhy_ml/4.png)   
* 第一步，找一个Model  
![](/img/lhy_ml/5.png)   

* 第二步，衡量f的好坏  
![](/img/lhy_ml/6.png)  
用loss function L来衡量f，L的输入是f，输出是f的好坏，由于f是由w,b构成的，也可以写成L(w,b)，所以f越好就是希望L越小，
使得L最小的f/ w,b记为f*/ w*,b*  

* 第三步，选择最好的f  
对于线性回归可以使用线性代数知识直接计算L的最小值，但无法直接计算其他问题    
在有了L之后只要对输入可以进行微分，就可以使用gradient descent来求解L的最小值  
![](/img/lhy_ml/7.png)   
gradient descent：随机w0,b0，计算L关于w,b的微分(切线斜率)，如果斜率为负，需要增大w，反之需要减小，所以我们将w,b向着梯度的反方向以学习率η倍数增加  

#### 1.2 gradient descent
###### GD的问题
![](/img/lhy_ml/8.png)   
1. 无法保证找到的是global minima  
2. 有可能梯度=0时是saddle point  
3. 有时梯度非常小时，它可能只是一个离minima比较远的平滑的部分  
* 不过，线性回归问题的梯度都是碗型，不存在这些问题

###### tip1:tuning learning rate
![](/img/lhy_ml/17.png)   
Adagrad更新lr方式如上图，那么其中分母的意义是什么呢？
![](/img/lhy_ml/18.png)   
从直观上说，分母式子衡量了造成反差的效果   

###### tip2:SGD
![](/img/lhy_ml/19.png)  
L只计算一个点
![](/img/lhy_ml/20.png)   
再GD计算所有点(20个点)后更新一次的时间里，SGD可以更新20次，速度更快

###### tip3:Feature Scaling
![](/img/lhy_ml/21.png)  ![](/img/lhy_ml/22.png)  
Loss呈现椭圆形时，各参数学习率不同，梯度下降不会直接奔向最低点  

#### 1.3 Regularization
* 更多model选择：  
![](/img/lhy_ml/9.png)   
更复杂的model在训练集上可以获得更小的error
![](/img/lhy_ml/10.png)   
但是在测试集上可能表现不好，出现overfitting现象  

* 解决办法：
1. 重新设计model  
![](/img/lhy_ml/11.png) 
![](/img/lhy_ml/12.png)   
这个model仍然是linear model，linear model是指参数对于output是否是线性，同理b+w1x1+w2x1<sup>2</sup>也是线性模型  

2. 正则化
![](/img/lhy_ml/13.png)   
* 正则化修改了L，在原来的基础上增加了一项，要求Lmin就是希望原来loss小的同时要选w很小的f，也就是平滑的f，平滑意味着输入有变化时，输出变化小，之所以要这样要求是因为多数情况下平滑的f更可能是较好的f  
* 为什么不对b正则化？因为b本身是一条直线，对f的平滑程度无影响，对它正则化就是要求b接近0  
* λ越大，f越平滑， 一般对λ取值0.01~0.05之间  

#### 1.4 Underfitting and Overfitting
![](/img/lhy_ml/14.png)   
把真正的f<sup>^</sup>看作靶心，其他f看作靶的其他位置，bias、variance如图，一个model是很多f的集合，也就是靶上的一个范围，不同数据同一个model下会找到不同的f* ，也就是在这个范围里选不同的f做f* ，如果这个model比较复杂，那就是它的范围就会比较大，这个大的范围更有可能包含真正的靶心f<sup>^</sup>，在这个范围里的f* 的平均情况下得到的f<sup>-</sup>会更接近f<sup>^</sup>，也就是瞄的比较准，bias比较小，但是由于范围大，f* 可能会散落在整个范围的各个位置，导致variance比较大，同理，简单的model范围小，bias较大，variance较小
![](/img/lhy_ml/15.png)   
error(E<sub>out</sub>)由bias和variance构成，如果错误主要来源于bias，说明underfitting，如果主要来源于variance说明overfitting，也就是说，如果model不能fit训练集，那么有较大的bias->underfitting，如果可以fit训练集但是在测试集上有较大误差，那么有较大的variance->overfitting，通过知道error的来源，来提升model    
* 如果underfitting，那么增加模型复杂度、增加更多features作为输入
* 如果overfitting，那么加大数据(自己造数据等方法)、正则化，但正则化可能会伤害到bias

#### 1.5 Model Selection
![](/img/lhy_ml/16.png)   
如果直接用测试集选模型，就污染了测试集，在测试集上的表现就不能体现真实外部表现，应该用验证集选择模型，这时选出的模型在测试集上的表现更能近似外部情况，验证集选择模型后可用所有训练数据再次训练选好的模型。为防止训练集测试集划分带来的问题，可以使用交叉验证N-fold Cross Validation的方法

#### 1.6 Summary
1. 选择一个model
2. 判断一个f好坏/选择一个Loss functiong
3. 选出一个f* ：梯度下降 
4. 验证集验证，根据验证集与训练集的error情况，判断是underfitting还是overfitting，回1

#### 1.7 预测PM2.5实例

```python3
import csv, os
import numpy as np
import matplotlib.pyplot as plt
from numpy.linalg import inv
import random
import math
import sys


def ada(X, Y, w, eta, iteration, lambdaL2):
    # len(X[0]):一笔资料有多少个特征，len(X)：有多少笔资料
    s_grad = np.zeros(len(X[0]))
    list_cost = []
    for i in range(iteration):
        # w = np.zeros(len(X[0]))列向量, X每一行是一笔资料, dot(X,w)得到所有输入的结果矩阵
        hypo = np.dot(X,w)
        loss = hypo - Y
        cost = np.sum(loss**2)/len(X)
        # append是加了一行进去(构成列向量)，这一行可能是一维的可能是多维的
        list_cost.append(cost)
        
        # L(w,b)=∑(y-(b+w·x))**2/n, x表示一笔资料，有n笔资料  
        # grad=∑2(y-(b+w·x))(-x)/n=X.T·loss/len(X)
        # 正则化：+lamda*(w)**2(他可能写错了，应该是平方)
        grad = np.dot(X.T, loss)/len(X) + lambdaL2*w
        
        # Adagrad更行学习率公式
        s_grad += grad**2
        ada = np.sqrt(s_grad)
        w = w - eta*grad/ada
    return w, list_cost


def SGD(X, Y, w, eta, iteration, lambdaL2):
    list_cost = []
    for i in range(iteration):
        hypo = np.dot(X,w)
        loss = hypo - Y
        cost = np.sum(loss**2)/len(X)
        list_cost.append(cost)

        rand = np.random.randint(0, len(X))
        # 只算随机的一笔资料(应该是乘以w**2)
        grad = X[rand]*loss[rand]/len(X) + lambdaL2*w
        w = w - eta*grad
    return w, list_cost

def GD(X, Y, w, eta, iteration, lambdaL2):
    list_cost = []
    for i in range(iteration):
        hypo = np.dot(X,w)
        loss = hypo - Y
        cost = np.sum(loss**2)/len(X)
        list_cost.append(cost)

        grad = np.dot(X.T, loss)/len(X) + lambdaL2 * w
        w = w - eta*grad
    return w, list_cost



# 每一个维度储存一种污染物的咨询
data = []
for i in range(18):
    data.append([])


#read data
n_row = 0
text = open('data/train.csv', 'r', encoding='big5')
row = csv.reader(text, delimiter=',')
for r in row:
    if n_row != 0:
        for i in range(3,27):
            if r[i] != "NR":
                data[(n_row-1)%18].append(float(r[i]))
            else:
                data[(n_row-1)%18].append(float(0))
    n_row = n_row + 1
text.close


#parse data to trainX and trainY
x = []
y = []
for i in range(12):
    for j in range(471):
        x.append([])
        for t in range(18):
            for s in range(9):
                x[471*i + j].append(data[t][480*i+j+s])
        y.append(data[9][480*i+j+9])
trainX = np.array(x) #每一行有9*18个数 每9个代表9天的某一种污染物
trainY = np.array(y)

#parse test data
test_x = []
n_row = 0
text = open('data/test.csv' ,"r")
row = csv.reader(text , delimiter= ",")

for r in row:
    if n_row %18 == 0:
        test_x.append([])
        for i in range(2,11):
            test_x[n_row//18].append(float(r[i]) )
    else :
        for i in range(2,11):
            if r[i] !="NR":
                test_x[n_row//18].append(float(r[i]))
            else:
                test_x[n_row//18].append(0)
    n_row = n_row+1
text.close()
test_x = np.array(test_x)

#parse anser
ans_y = []
n_row = 0
text = open('data/ans.csv', "r")
row = csv.reader(text, delimiter=",")

for r in row:
    ans_y.append(r[1])

ans_y = ans_y[1:]
ans_y = np.array(list(map(int, ans_y)))


# add bias
# concatenate：连接
test_x = np.concatenate((np.ones((test_x.shape[0],1)),test_x), axis=1)
trainX = np.concatenate((np.ones((trainX.shape[0],1)), trainX), axis=1)


#train data
w = np.zeros(len(trainX[0]))
w_sgd, cost_list_sgd = SGD(trainX, trainY, w, eta=0.0001, iteration=20000, lambdaL2=0)
# w_sgd50, cost_list_sgd50 = SGD(trainX, trainY, w, eta=0.0001, iteration=20000, lambdaL2=50)
w_ada, cost_list_ada = ada(trainX, trainY, w, eta=1, iteration=20000, lambdaL2=0)
# w_gd, cost_list_gd = GD(trainX, trainY, w, eta=0.0001, iteration=20000, lambdaL2=0)

#close form 闭式解/解析解
# inv:求逆 
w_cf = inv(trainX.T.dot(trainX)).dot(trainX.T).dot(trainY)
cost_wcf = np.sum((trainX.dot(w_cf)-trainY)**2) / len(trainX)
hori = [cost_wcf for i in range(20000-3)]

#output testdata
y_ada = np.dot(test_x, w_ada)
y_sgd = np.dot(test_x, w_sgd)
y_cf = np.dot(test_x, w_cf)

#csv format
ans = []
for i in range(len(test_x)):
    ans.append(["id_"+str(i)])
    a = np.dot(w_ada,test_x[i])
    ans[i].append(a)

filename = "result/predict.csv"
text = open(filename, "w+")
s = csv.writer(text,delimiter=',',lineterminator='\n')
s.writerow(["id","value"])
for i in range(len(ans)):
    s.writerow(ans[i])
text.close()


#plot training data with different gradiant method
plt.plot(np.arange(len(cost_list_ada[3:])), cost_list_ada[3:], 'b', label="ada")
plt.plot(np.arange(len(cost_list_sgd[3:])), cost_list_sgd[3:], 'g', label='sgd')
# plt.plot(np.arange(len(cost_list_sgd50[3:])), cost_list_sgd50[3:], 'c', label='sgd50')
# plt.plot(np.arange(len(cost_list_gd[3:])), cost_list_gd[3:], 'r', label='gd')
plt.plot(np.arange(len(cost_list_ada[3:])), hori, 'y--', label='close-form')
plt.title('Train Process')
plt.xlabel('Iteration')
plt.ylabel('Loss Function(Quadratic)')
plt.legend()
plt.savefig(os.path.join(os.path.dirname(__file__), "figures/TrainProcess"))
plt.show()

#plot fianl answer
plt.figure()
plt.subplot(131)
plt.title('CloseForm')
plt.xlabel('dataset')
plt.ylabel('pm2.5')
plt.plot(np.arange((len(ans_y))), ans_y, 'r,')
plt.plot(np.arange(240), y_cf, 'b')
plt.subplot(132)
plt.title('ada')
plt.xlabel('dataset')
plt.ylabel('pm2.5')
plt.plot(np.arange((len(ans_y))), ans_y, 'r,')
plt.plot(np.arange(240), y_ada, 'g')
plt.subplot(133)
plt.title('sgd')
plt.xlabel('dataset')
plt.ylabel('pm2.5')
plt.plot(np.arange((len(ans_y))), ans_y, 'r,')
plt.plot(np.arange(240), y_sgd, 'b')
plt.tight_layout()
plt.savefig(os.path.join(os.path.dirname(__file__), "figures/Compare"))
plt.show()

```
## Reference
* 台大李宏毅老师机器学习课程  
* [1.7实现 https://github.com/maplezzz/ML2017S_Hung-yi-Lee_HW](https://github.com/maplezzz/ML2017S_Hung-yi-Lee_HW)









