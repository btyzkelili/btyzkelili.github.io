---
layout:     post
title:      "Structure Learning"
subtitle:   "Introduction"
date:       2019-09-04
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - SVM
---  
## Structure Learning
![](/img/lhy_ml/structure-1.jpg)  
之前的模型都是输入一个vector输出另一个vector，现在输入和输出可能是其他形式：Sequence,tree structure,
bounding box,paragraph等

Structure Learning的unified形式，训练时，F的输入是X,Y，输出常数R，X,Y越匹配输出的R越大，测试时，输入X找让F(x,y)
结果最大的y(穷举所有y)，也就是和x最匹配的y

![](/img/lhy_ml/structure-2.jpg)  
有一个任务是在图片中圈出人物"Haruhi"训练时，让正确的图片圈法分数最高，测试时，穷举所有圈的方法，找到得分最高的圈发

其他任务举例：  
![](/img/lhy_ml/structure-3.jpg)  
![](/img/lhy_ml/structure-4.jpg)  

![](/img/lhy_ml/structure-5.jpg)  
可以看做是几率形式
![](/img/lhy_ml/structure-6.jpg)  
有的时候任务说成几率有些奇怪，几率,有限制1，需要花时间nomolization，但几率容易想象理解

![](/img/lhy_ml/structure-7.jpg)  
![](/img/lhy_ml/structure-8.jpg)  
![](/img/lhy_ml/structure-9.jpg)  
![](/img/lhy_ml/structure-10.jpg)  
要想做到Structure Learning需要解决上面三个问题，之前讲的DNN是structure learning的特例

![](/img/lhy_ml/structure-11.jpg)  
对比DNN，DNN是Structure Learning的特例，图中CE指cross entropy






