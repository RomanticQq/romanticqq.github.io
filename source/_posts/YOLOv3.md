---
title: YOLOv3
abbrlink: 13592
date: 2022-05-17 00:09:25
tags:
  - YOLO
  - 深度学习
categories: 深度学习算法
mathjax: true
---

### Darknet53

YOLOv3采用了Darknet53为主干网络；

### 多scale

在YOLOv3上设计了3种scale，分别为特征图大小13 * 13、26 * 26、52 * 52上进行大、中、小目标预测；

### 网络结构

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220517124109.png)

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220517122901.png)

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220517124855.jpg)

### Residual module

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220517123021.png)

残差网络，会有A(保存原来的不进行任何操作),B两种通道，然后再合并，即使F(x)不起作用，还会保存以前的输出结果。

**注：**使用残差网络，不能保证效果一定有多大提升，但是至少不会差。

### 输出

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220517152650.jpg)

- YOLOv3网络的输入尺寸为 (m,416,416,3), 其中m代表每个batch中图像数目,m=1,代表每个batch处理1张输入图像；
- YOLOv3分3个尺度进行预测, 3个尺度的特征图的大小依次为13X13,26X26以及52X52；
- YOLOv3中每个cell预测3个bounding box,每个bounding box 可以表示为6元组 ![[公式]](https://www.zhihu.com/equation?tex=%28t_x%2Ct_y%2Ct_w%2Ct_h%2Cp_c%2Cc%29) ；
- 在COCO数据集中一共有80个类别,此时我们将c扩展成80维向量,这样我们每个bounding box可以用85维向量进行表示；
- 特征图大小为13 * 13，可以预测169(13 * 13)个物体，然后依次类推；

### 先验眶的生成

先使用K-means方法生成9个先验框，然后按照大小进行排序，分给3个不同的scale。

### logistic

Softmax实现物体单分类最后的评判， Softmax能够确保所有物体的预测概率之和为1，比如一个物体的预测是狗的概率是80%，那么是其他物体的概率之和为20%。这就是单标签概率。

然后，对于多标签预测，比如，一个物体是狗的概率是80%，是狼狗的概率是70%，是猎狗的概率是75%，像这样的分类判决，Softmax就无法胜任了。

YOLO V3使用了logistic激活函数替换了softmax函数，把物体的联合的多分类，变成独立的二分类，从而实现对物体多标签的支持
([此部分参考YOLO V3 - 网络结构、原理、改进的全新、全面、通俗、结构化讲解](https://blog.csdn.net/HiWangWenBing/article/details/122226224))

##### 逻辑回归中的基本构造函数

在逻辑回归算法中，选用的基本函数就是sigmoid函数
$$
y=\frac{1}{1+e^{-x}}
$$


该函数用于预测输入x后标签y的概率，注意，这里的x并非是数据集的原始数据输入，而是乘以了参数θ之后的值，即 x = X ⋅ θ,因此逻辑回归的基本函数为：
$$
y=\frac{1}{1+e^{-θx}}
$$

