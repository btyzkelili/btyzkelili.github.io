---
layout:     post
title:      "林轩田-机器学习基石-作业3-4"
subtitle:   ""
date:       2019-07-17
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 林轩田:机器学习基石
---
## 作业三
---
#### 3-13 linear regression
* 在[-1,1]上生成1000个点，并且用f=sign(x1<sup>2</sup> + x2<sup>2</sup> - 0.6) 得到其标签，再加上10%的噪声，用线性回归方式训练1000次，
计算其平均错误率E<sub>in</sub>(训练集上的错误率)  
```   
    import random
    import numpy as np


    # target function f(x1, x2) = sign(x1^2 + x2^2 - 0.6)
    def target_function(x1, x2):
        if (x1 * x1 + x2 * x2 - 0.6) >= 0:
            return 1
        else:
            return -1


    # create train_set
    def training_data_with_random_error(num=1000):
        features = np.zeros((num, 3))
        labels = np.zeros((num, 1))

        points_x1 = np.array([round(random.uniform(-1, 1), 2) for i in range(num)])
        points_x2 = np.array([round(random.uniform(-1, 1), 2) for i in range(num)])

        for i in range(num):
            # create random feature
            features[i, 0] = 1
            features[i, 1] = points_x1[i]
            features[i, 2] = points_x2[i]
            labels[i] = target_function(points_x1[i], points_x2[i])
            # choose 10% error labels
            if i <= num * 0.1:
                if labels[i] < 0:
                    labels[i] = 1
                else:
                    labels[i] = -1
        return features, labels


    def error_rate(features, labels, w):
        wrong = 0
        for i in range(len(labels)):
            if np.dot(features[i], w) * labels[i, 0] < 0:
                wrong += 1
        return wrong / (len(labels) * 1.0)


    def linear_regression_closed_form(X, Y):
        """
            linear regression:
            model     : g(x) = Wt * X
            strategy  : squared error
            algorithm : close form(matrix)
            result    : w = (Xt.X)^-1.Xt.Y
            线性回归直接使用公式
        """
        return np.linalg.inv(np.dot(X.T, X)).dot(X.T).dot(Y)


    if __name__ == '__main__':
        error_rate_array = []
        for i in range(1000):
            (features, labels) = training_data_with_random_error(1000)
            w13 = linear_regression_closed_form(features, labels)
            error_rate_array.append(error_rate(features, labels, w13))

        # error rate, approximately 0.5
        avr_err = sum(error_rate_array) / (len(error_rate_array) * 1.0)

        print("Linear regression for classification without feature transform:Average error--", avr_err)
```

#### 3-14 特征转换
* 上一题的基础上，增加特征转换处理(1,x1,x2,x1x2,x1<sup>2</sup>,x2<sup>2</sup>)，再次计算得到最佳的**w**   
   
 ```
     def feature_transform(features):
        new = np.zeros((len(features), 6))
        new[:, 0:3] = features[:, :] * 1//前三位和原来的一样
        new[:, 3] = features[:, 1] * features[:, 2]//x1x2
        new[:, 4] = features[:, 1] * features[:, 1]//x1<sup>2</sup>
        new[:, 5] = features[:, 2] * features[:, 2]//x2<sup>2</sup>
        return new
```

#### 3-18 logistic regression
* 下载训练样本和测试样本,进行逻辑回归。取迭代步长ita = 0.001/0.01,使用或不适用随机梯度下降,迭代次数T=2000(训练2000轮)，求E_out   
```
    import numpy as np


    def data_load(file_path):
        # open file and read lines
        f = open(file_path)
        try:
            lines = f.readlines()
        finally:
            f.close()

        # create features and labels array
        example_num = len(lines)
        feature_dimension = len(lines[0].strip().split())

        features = np.zeros((example_num, feature_dimension))
        features[:, 0] = 1
        labels = np.zeros((example_num, 1))

        for index, line in enumerate(lines):
            # items[0:-1]--features   items[-1]--label
            items = line.strip().split(' ')
            # get features
            features[index, 1:] = [float(str_num) for str_num in items[0:-1]]

            # get label
            labels[index] = float(items[-1])

        return features, labels


    # gradient descent
    def gradient_descent(X, y, w):
        # -YnWtXn
        tmp = -y * (np.dot(X, w))

        # θ(-YnWtXn) = exp(tmp)/1+exp(tmp)
        # weight_matrix = np.array([math.exp(_)/(1+math.exp(_)) for _ in tmp]).reshape(len(X), 1)
        weight_matrix = np.exp(tmp) / ((1 + np.exp(tmp)) * 1.0)
        gradient = 1 / (len(X) * 1.0) * (sum(weight_matrix * -y * X).reshape(len(w), 1))

        return gradient


    # gradient descent 只计算一个点的梯度
    def stochastic_gradient_descent(X, y, w):
        # -YnWtXn
        tmp = -y * (np.dot(X, w))

        # θ(-YnWtXn) = exp(tmp)/1+exp(tmp)
        # weight = math.exp(tmp[0])/((1+math.exp(tmp[0]))*1.0)
        weight = np.exp(tmp) / ((1 + np.exp(tmp)) * 1.0)

        gradient = weight * -y * X
        return gradient.reshape(len(gradient), 1)


    # LinearRegression Class
    class LinearRegression:

        def __init__(self):
            pass

        # fit model
        def fit(self, X, y, Eta=0.001, max_iteration=2000, sgd=False):
            # ∂E/∂w = 1/N * ∑θ(-YnWtXn)(-YnXn)
            self.__w = np.zeros((len(X[0]), 1))

            # whether use stochastic gradient descent
            if not sgd:
                for i in range(max_iteration):
                    self.__w = self.__w - Eta * gradient_descent(X, y, self.__w)
            else:
                index = 0
                for i in range(max_iteration)://训练轮次为2000
                    if (index >= len(X)):
                        index = 0
                    //选择一个点计算梯度
                    self.__w = self.__w - Eta * stochastic_gradient_descent(np.array(X[index]), y[index], self.__w)
                    index += 1

        # predict
        def predict(self, X):
            binary_result = np.dot(X, self.__w) >= 0
            return np.array([(1 if _ > 0 else -1) for _ in binary_result]).reshape(len(X), 1)

        # get vector w
        def get_w(self):
            return self.__w

        # score(error rate)
        def score(self, X, y):
            predict_y = self.predict(X)
            return sum(predict_y != y) / (len(y) * 1.0)


    if __name__ == '__main__':
        # 18
        # training model
        (X, Y) = data_load("hw3_train.dat")
        lr = LinearRegression()
        lr.fit(X, Y, max_iteration=2000)

        # get 0/1 error in test data
        test_X, test_Y = data_load("hw3_test.dat")
        print("E_out: ", lr.score(test_X, test_Y))
```
