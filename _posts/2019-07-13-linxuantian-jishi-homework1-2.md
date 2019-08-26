---
layout:     post
title:      "林轩田-机器学习基石-作业1-2"
subtitle:   ""
date:       2019-07-13
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
## 作业一
---
#### 1-1

![](/img/linxuant-jishi/t-1-1.PNG)    

* 题意：下列哪些问题最适合用机器学习解决

* 分析：适合用机器学习解决的问题主要包括以下特点
  
              a.存在某些目标，隐藏规则（underlying pattren）
              b.这些规则我们难以定义，不知道如何写下了
              c.有学习这个隐藏规则的资料data
  
  i.区分一个数是否为素数：错误，我们可以很简单写出素数的规则，只能被1或他本身整除
  
  ii.确定信用卡是否被盗刷：正确，这是极其学习里面的异常点检测问题
  
  iii.确定一个物体的落地时间：错误，这里有物理学公式，h=0.5*g*t^2
  
  iv.确定拥挤路口交通信号灯的最佳循环：正确
  
  v.确定某种药物的推荐服用者年龄：正确，可以通过聚类找出效果好的群

* 答案：ii，iv,v

#### 1-5

![](/img/linxuant-jishi/t-1-5.PNG)   

* 题意：有选择的在小白鼠上安排实验，快速知道癌症药的潜在作用

* 分析：机器有问问题的能力，希望能通过有技巧问问题来用更少的标记学习，常用在取得标记很贵的场合。
  
  在某些情况下，没有类标签的数据相当丰富而有类标签的数据相当稀少，并且人工对数据进行标记的成本又相当高昂。在这种情况下，我们可以让学习算法主动地提出要对哪些数据进行标注，之后我们要将这些数据送到专家那里让他们进行标注，再将这些数据加入到训练样本集中对算法进行训练。这一过程叫做主动学习。
  
  主动学习方法一般可以分为两部分： 学习引擎和选择引擎。学习引擎维护一个基准分类器，并使用监督学习算法对系统提供的已标注样例进行学习从而使该分类器的性能提高，而选择引擎负责运行样例选择算法选择一个未标注的样例并将其交由人类专家进行标注，再将标注后的样例加入到已标注样例集中。学习引擎和选择引擎交替工作，经过多次循环，基准分类器的性能逐渐提高，当满足预设条件时，过程终止。

* 答案：active learning

#### 1-8
![](/img/linxuant-jishi/t-1-8.PNG)   

* 分析：没有免费午餐定理(学习算法不能脱离实际问题)

* 答案：最后一项

#### 1-12
![](/img/linxuant-jishi/t-1-12-1.PNG)   
![](/img/linxuant-jishi/t-1-12-2.PNG)   

* 题意：利用Hoeffding Inequality计算 当u=0.9时v小于等于0.1的概率

* 分析：Hoeffding Inequality为 P（[v-u] 大于 epsilon） 小于等于 2* e^(-2*N*epsilon^2),N为抽样个数，带入计算就可以了

* 答案：5.52 * 10^(-6)

#### 1-15~1-17 PLA算法

```python

class DataSet:

    def __init__(self, filename):
	self.input = []
	self.output = []
	self.load_data(filename)

    def load_data(self, filename):
	with open(filename) as csvfile:
	    reader = csv.reader(csvfile, delimiter='\t')
	    for line in reader:
		x = line[0].split()
		x.insert(0, '1')
		y = line[1]
		self.input.append(x)
		self.output.append(y)


class PLA:
    def __init__(self, train_name='hw1_15_train.dat', test_name=None):
	self.train_set = DataSet(train_name)
	if test_name:
	    self.test_set = DataSet(test_name)

    def random_cycle_pla(self, times=2000, eta=1, print_out=False):
	total_updates = 0
	data_set = list(zip(self.train_set.input, self.train_set.output))
	for idx, _ in enumerate(range(times)):
	    shuffle(data_set)
	    current_updates = self.naive_pla(data_set, eta, print_out)
	    total_updates += current_updates
	return total_updates / times

    def naive_pla(self, data_set=None, eta=1, print_out=False):
	"""naive perceptron learning algorithm"""
	current_updates = 0
	w = np.zeros(5)
	if not data_set:
	    data_set = list(zip(self.train_set.input, self.train_set.output))
	while True:
	    halt = True
	    for item in data_set:
		x = np.array(item[0], dtype=float)
		y = np.array(item[1], dtype=int)
		if sign(w.dot(x)) != y:
		    current_updates += 1
		    w += eta * y * x
		    halt = False
	    if halt:
		break
	if print_out:
	    print(f'第{idx}次终止次数：{current_updates}')
	return current_updates
```

#### 1-18~1-20 Pocket算法

* 注意：每次找到不符合条件的点之后，pocket时会更新w的，但是只有当前w比pocket_w的错误率更小的时候才会更新pocket_w

```python
		
def errors_count(self, w, data_set):
	""""统计errors发生次数"""
	count = 0
	for x, y in data_set:
	    x = np.array(x, dtype=float)
	    y = np.array(y, dtype=int)
	    if sign(w.dot(x)) != y:
		count += 1
	return count
def pocket_algorithm(self, update_times=50, pocket=True):
	"""pocket=True： 返回pocketWeight
	否则返回w"""
	data_set = list(zip(self.train_set.input, self.train_set.output))
	updates = 0
	w = np.zeros(5)
	pocket_weight = np.zeros(45)
	min_errors = sys.maxsize
	halt = False
	while not halt:
	    shuffle(data_set)
	    for item in data_set:
		x = np.array(item[0], dtype=float)
		y = np.array(item[1], dtype=int)
		if sign(w.dot(x)) != y:
		    w = w + y * x  # w每次都更新
		    updates += 1
		    # print(f'updates: {updates}')
		    errors_count = self.errors_count(w, data_set)
		    if errors_count < min_errors:
			min_errors = errors_count
			pocket_weight = w  # pocket_weight只有遇到更好的w才更新
		if updates >= update_times or min_errors == 0:
		    halt = True
		    break
	return pocket_weight if pocket else w
```

## 作业二
#### 2-1
![](/img/linxuant-jishi/t-2-1.png)  
* 题意：目标函数f的错误率为mu，在样本上加了噪声使得p(x/y)如上面公式（这里1-lambda就是噪声比例,由于输出y是二元的，所以加噪声的意思就是把原来的f（x）变号，成为y），求一个hyphothesis  h的有噪声的y的错误率。

* 分析：这里解决的是二元分类问题，即y={-1，+1}。那么这里加噪声的意思就是1-lamba比例的（x,y）变成（x,-y）了。 

当y=f（x）时，由题意我们知道h对f的错误率为mu，而y=f(x)概率为lambda，所以这部分的错误率为lambda*mu。

当y不等于f(x)时，由于我们只是把y的符号翻转了，所以原来正确的变成错误的，原来错误的变成正确的，故此处h对f的错误率为1-mu,这部分错误率为（1-lambda）(1-mu)

* 答案：第三项

#### 2-3
![](/img/linxuant-jishi/t-2-3.png)  
* 题意：当N大于等于2，d_vc大于等于2时，我们可以用N^d_vc代替mH(N)。当d_vc = 10时，你想要95%的置信率，代表epsilon小于等于0.05，那么我们需要多要样本（N）？
* 分析:![](/img/linxuant-jishi/t-2-3-1.png)  
* 答案：460,000

#### 2-4
![](/img/linxuant-jishi/t-2-4.png)  
* 题意：d_vc=50，置信率为1-delta,delta = 0.05,训练样本数为N。当N = 10000时，分别用下面五个公式计算epsilon的值，哪个最小（最紧）？
* 分析：当N>=2,d<sub>vc</sub>>=2时，m<sub>H</sub>(N)<=N<sup>d<sub>vc</sub></sup>
* 答案： Decoroye

#### 2-6
![](/img/linxuant-jishi/t-2-6.png)  
* 题意：positive and negatibe intervals on R的mH(N)为多少？
* 分析：对于positive interval,N个点将R(x轴)划分为N+1个区间，任选两个点作为边界：C<sub>N+1</sub><sup>2</sup>种，再加上1个没有内部正值的情况，共C<sub>N+1</sub><sup>2</sup>+1，加上negative interval就是乘以2，还要减去重复计算的，左边全是负右边全是正的N-1种，和左边全是正右边全是负的N-1种，所以结果为C<sub>N+1</sub><sup>2</sup>+1-2(N-1)=N<sup>2</sup>-N+2

#### 2-8
![](/img/linxuant-jishi/t-2-8.png)    
* 题意：利用x1^2+x2^2作为分类线，形成两个同心圆，在同心圆里面的归为+1类，在同心圆外面的归为-1类。假设有N个样本，求mH(N)
* 分析：二维positive Interval
* 答案：最后一项

#### 2-9
![](/img/linxuant-jishi/t-2-9.png)    
* 题意：Hyphothesis如上面图所示，求H得d_vc
* 分析：从H可以看出，这道题就是perceptrons，课堂上已经证明过其d_vc = D+1
* 答案：D+1

#### 2-10
![](/img/linxuant-jishi/t-2-10.png)   
* 题意：s是一个d维向量的集合，而且每个d维向量对应一个+1或一个-1。求其VC-dimension
* 分析：无论N多大，s中d维的向量(这个向量的每一位只能是0/1)最多有2<sup>d</sup>，每一个d维的向量可以对应+1/-1，一共有2<sup>2<sup>d</sup></sup>种可能，所以VC-dimension = 2<sup>d</sup>(?)
* 答案：第一项

#### 2-11
![](/img/linxuant-jishi/t-2-11.png)  
* 题意：H的定义如上图，求H得d_vc
* 分析：三角波，参数控制的是波的周期，因此所有N都能shatter(?)
* 答案：无穷

#### 2-12
![](/img/linxuant-jishi/t-2-12.png)   
* 题意：下列哪些式子是成长函数mH（N）的上限函数，当N大于等于d_vc大于等于2
* 分析：选项1：括号内的不会比是N的时候大，因此不可能是mH(N)mH(N)的上界； 选项2：这是个常数，不可能是上界； 
选项3：m<sub>H</sub>(N)的一个上界是2<sip>N</sup>，2<sup>i</sup>m<sub>H</sub>(N−i)对应过去的上界就是2<sup>i</sup>⋅2<sup>(N−i)</sup>=2N ;选项4：N<sub>dvc</ub>是mH(N)的上界，但是开平方就不一定了。
* 答案：第三项

#### 2-13
![](/img/linxuant-jishi/t-2-13.png)  
* 题意：下面哪些mH(N)是不可能的
* 分析：(N)是单增的，而第四项并不是，第四项有平整，有突增。
* 答案：第四项

#### 2-14
![](/img/linxuant-jishi/t-2-14.png)   
* 题意：下面这些选项中有的是正确的，有的是错误的。在正确的选项中找到范围最小的。
* 分析：这道题求的是并集合的d_vc。
                   首先，我们看左边边界。若有一个Hk是空集，那么d_vc=0,所以最小值是0
                   之后，我们看右边边界。由于是交集，我们最多保留最小的d_vc
* 答案：第四项

#### 2-15
![](/img/linxuant-jishi/t-2-15.png)   
* 题意：在考虑了交集情况，讨论并情况
* 分析：a.左边：H1...Hk能做的并集也能做，故为max
        b.右边的问题是有没有K-1。试想，有一个H1，把平面所有点分为+1，H2把平面所有点分为-1。H1并H2的话为VC dimension为1，而各自d_vc加起来为0(?)
* 答案：第四项

#### 2-16
![](/img/linxuant-jishi/t-2-16.png)   
* 题意：“positive and negative rays”:mH（N）=2N。在区间[-1，1]上取N个点，考虑s不重复时，theta可以取在N-1个内部间隔，s=1/-1，所以有2(N-1)，再加上全是0和全是1的两种情况，共有2N种情况。对于h:选一个位置为theta，在s=1时，比theta大的点是1,比theta小的是0，在s=-1时，比theta大的点是0,比theta小的是1，而真正的f是theta=0的情况。现在我们要计算h下的E<sub>out</sub>
* 分析：由2-1知道加噪声后的计算方式。这道题加20%噪声，所以lambda = 0.8,我们只要求mu就可以了。mu的定义是h（x）与f(x)的不同，即错误率。f(x)=s（x）=sign(x),h(x)=s * sign（x-theta),根据s和theta分类讨论:
	1.s = 1, theta > 0:错误率为theta/2
        2.s=1，theta < 0;错误率为|theta|/2
        3.s=-1,theta > 0:错误率为 （2 - theta）/2
        4.s=-1,theta <0:错误率为（2- | theta |）/2
        综上，s=1 错误率为 |theta|/2;s = -1，错误率为（2-|theta|）/2
        利用一个式子写出来： mu = (s+1)/2 * (|theta|/2) -  (s-1)/2 * ((2-|theta|)/2)
       最后 E_out = mu * lambda + (1 - lambda) * (1 - mu)，lambda = 0.8,mu带入可以得到答案
* 答案：0.5+0.3*s*(|theta| - 1)

#### 2-17 2-18
![](/img/linxuant-jishi/t-2-17-18.png)   
* 17题自己随机在[-1,1]抽取20个点，对于2* 20个h，分别计算他们的E<sub>in</sub>，得到最小的
* 18题，在17题的基础上用16题的结论计算E<sub>out</sub>

```python
import numpy as np
import random
class decisonStump(object):
    def __init__(self,dimension,data_count,noise):
	self.dimension=dimension
	self.data_count=data_count
	self.noise=noise
    def generate_dataset(self):
	dataset=np.zeros((self.data_count,self.dimension+1))
	for i in range(self.data_count):
	    x=random.uniform(-1,1)
	    line=[]
	    line.append(x)
	    y=np.sign(x)*np.sign(random.uniform(0,1)-self.noise)
	    line.append(y)
	    dataset[i:]=line
	return dataset
    def get_theta(self,dataset):
	l=np.sort(dataset[:,0])
	theta=np.zeros((self.data_count,1))
	for i in range(self.data_count-1):
	    theta[i]=(l[i]+l[i+1])/2
	theta[-1]=1
	return theta
    def question1718(self):
	sum_e_in = 0
	sum_e_out=0
	for i in range(5000):
	    dataset = self.generate_dataset()
	    theta=self.get_theta(dataset)
	    e_in = np.zeros((2, self.data_count))
	    for j in range(self.data_count):#直接数组计算，省略循环
		a=dataset[:,1]*np.sign(dataset[:,0]-theta[j])# dataset[:,1]是真实的y，np.sign(dataset[:,0]-theta[j])是h预测出的y
		e_in[0][j] = (self.data_count - np.sum(a)) / (2 * self.data_count)  # 数组只有-1和+1，可直接计算出-1所占比例,-1就是预测错误的
		e_in[1][j] = (self.data_count - np.sum(-a)) / (2 * self.data_count)
	    min0, min1 = np.min(e_in[0]), np.min(e_in[1])
	    s=0
	    theta_best=0
	    if min0 < min1:
		s = 1
		theta_best = theta[np.argmin(e_in[0]),0]
		sum_e_in+=min0
	    else:
		s = -1
		theta_best = theta[np.argmin(e_in[1]),0]
		sum_e_in+=min1
	    e_out=0.5+0.3*s*(np.abs(theta_best)-1)
	    sum_e_out+=e_out
	print(sum_e_in/5000,sum_e_out/5000)


if __name__=='__main__':
    decision=decisonStump(1,20,0.2)
    decision.question1718()
```
#### 2-19 2-20
![](/img/linxuant-jishi/t-2-19.png)   
![](/img/linxuant-jishi/t-2-20.png)   
* 19题用老师的数据集，x是9维，每一维度都用2-17的方式得到最小E<sub>in</sub>的h,最后9个h里找到最小E<sub>in</sub>的h作为全局h
* 20题对最好的h用测试集计算E<sub>out</sub>  

```python
import numpy as np

class decisonStump(object):
    def get_train_dataset(self,path):
	with open(path,'r') as f:
	    rawData=f.readlines()
	dimension=len(rawData[0].strip().split(' '))-1
	data_count=len(rawData)
	data_set=np.zeros((data_count,dimension+1))
	for i in range(data_count):
	    data_set[i:]=rawData[i].strip().split(' ')
	return data_set,dimension,data_count
    def get_theta(self,dataset):
	data_count=len(dataset)
	l=np.sort(dataset)
	theta=np.zeros((data_count,1))
	for i in range(data_count-1):
	    theta[i]=(l[i]+l[i+1])/2
	theta[-1]=1
	return theta
    def question19(self):
	dataset,dimension,data_count=self.get_train_dataset('hw2_train.dat.txt')
	s1=[]
	theta_best1=[]
	E_in=[]
	for i in range(dimension):
	    theta=self.get_theta(dataset[:,i])
	    e_in = np.zeros((2, data_count))
	    for j in range(data_count):
		a=dataset[:,-1]*np.sign(dataset[:,i]-theta[j])
		e_in[0][j] = (data_count - np.sum(a)) / (2 * data_count)  # 数组只有-1和+1，可直接计算出-1所占比例
		e_in[1][j] = (data_count - np.sum(-a)) / (2 * data_count)
	    min0,min1=np.min(e_in[0,:]),np.min(e_in[1,:])
	    if min0>=min1:
		s1.append(-1)
		theta_best1.append(theta[np.argmin(e_in[1])])
	    else:
		s1.append(1)
		theta_best1.append(theta[np.argmin(e_in[0])])
	    E_in.append(np.min(np.min(e_in)))
	minS=s1[np.argmin(E_in)]
	minTheta=theta_best1[np.argmin(E_in)]
	print(np.min(E_in))
	return minS,minTheta
    def question20(self):
	s,theta=self.question19()
	dataset, dimension, data_count = self.get_train_dataset('hw2_test.dat.txt')
	E_out=[]
	for i in range(dimension):
	    a=dataset[:,-1]*np.sign(dataset[:,i]-theta)*s
	    e_out=(data_count-np.sum(a))/(2*data_count)
	    E_out.append(e_out)
	print(np.min(E_out))



if __name__=='__main__':
    decision=decisonStump()
    decision.question20()
```
