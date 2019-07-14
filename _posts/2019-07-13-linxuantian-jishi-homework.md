---
layout:     post
title:      "林轩田-机器学习基石-作业"
subtitle:   ""
date:       2019-07-13
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
# 作业一
---
### 1-1

![](/img/linxuant-jishi/t-1-1.png)    

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

### 1-5

![](/img/linxuant-jishi/t-1-5.png)   

* 题意：有选择的在小白鼠上安排实验，快速知道癌症药的潜在作用

* 分析：机器有问问题的能力，希望能通过有技巧问问题来用更少的标记学习，常用在取得标记很贵的场合。
  
  在某些情况下，没有类标签的数据相当丰富而有类标签的数据相当稀少，并且人工对数据进行标记的成本又相当高昂。在这种情况下，我们可以让学习算法主动地提出要对哪些数据进行标注，之后我们要将这些数据送到专家那里让他们进行标注，再将这些数据加入到训练样本集中对算法进行训练。这一过程叫做主动学习。
  
  主动学习方法一般可以分为两部分： 学习引擎和选择引擎。学习引擎维护一个基准分类器，并使用监督学习算法对系统提供的已标注样例进行学习从而使该分类器的性能提高，而选择引擎负责运行样例选择算法选择一个未标注的样例并将其交由人类专家进行标注，再将标注后的样例加入到已标注样例集中。学习引擎和选择引擎交替工作，经过多次循环，基准分类器的性能逐渐提高，当满足预设条件时，过程终止。

* 答案：active learning

### 1-8
![](/img/linxuant-jishi/t-1-8.png)   

* 分析：没有免费午餐定理(学习算法不能脱离实际问题)

* 答案：最后一项

### 1-12
![](/img/linxuant-jishi/t-1-12-1.png)   
![](/img/linxuant-jishi/t-1-12-2.png)   

* 题意：利用Hoeffding Inequality计算 当u=0.9时v小于等于0.1的概率

* 分析：Hoeffding Inequality为 P（[v-u] 大于 epsilon） 小于等于 2* e^(-2*N*epsilon^2),N为抽样个数，带入计算就可以了

* 答案：5.52 * 10^(-6)

### 1-15~1-17 PLA算法

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


### 1-18~1-20 Pocket算法

* 注意：每次找到不符合条件的点之后，pocket时会更新w的，但是只有当前w比pocket_w的错误率更小的时候才会更新pocket_w

		
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

