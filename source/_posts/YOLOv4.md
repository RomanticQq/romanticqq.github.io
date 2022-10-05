---
title: YOLOv4
tags:
  - YOLO
  - 深度学习
categories: 深度学习算法
mathjax: true
abbrlink: 63321
date: 2022-05-24 13:32:21
---

### Bag of freebies(BOF)

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524141933.png)

#### Mosaic data augmentation

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524141948.png)

Mixup：让两张图片的像素值对应相加，生成一张新的图片；

Cutout：对一张图片的部分进行遮挡；

CutMix：把多张图片进行缩放，拼接到一张图片上；

#### 数据增强

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524142001.png)

Random Erase：用随机值或训练集的平均像素替换图像的区域；

Hide and Seek：根据概率设置随机隐藏一些补丁；

### Self-adversarial-training(SAT)

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220609113938.png)

系数要足够小

### DropBlock

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220609114052.png)

之前是随机失活一个像素点，但是周围的像素点还存在，其实对整个图像的影响并不大；

现在随机吃掉一个区域，使网络的性能更好。

### Label Smoothing

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524142442.png)

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524142625.png)

平滑标签，不让边界感那么强，可以提高图像的识别率；

这个0.1的系数是自己设置的；

### IOU损失

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220609114132.png)

### GIOU损失

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524142827.png)

**重点：**是在不重叠的情况下，预测框向真实框前进，不重叠，不重叠！！！！

当重叠时，不能反应出来情况的好坏；

### DIOU损失

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524143429.png)

### CIOU损失

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524144750.PNG)

### DIOU-NMS

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220609114150.png)

### SOFT-NMS

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524150424.png)

先不直接剔除，而是降低置信度，再给一次机会。

### SPPNet

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524150602.png)

虽然输出的图像尺寸大小可能不一样，但是通过最大池化来满足最终输入特征图的大小是一样的。

### CSPNet

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524151021.png)

把特征图平均分成两部分，一部分什么都不做，另外一部分经过卷积进行输出，虽然精度上可能有所降低，但是速度上会加快很多，但是结果表现精度可能并没有降低，还有一点点升高。

### CBAM

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524151400.png)

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524151814.png)

Channel Attention Module:对不同特征图产生一个概率，这个概率值表示对不同特征图的关注度；

SAM：对于特征图的不同位置的注意力机制；

### PAN

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524151909.png)



![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524151930.png)

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524152214.png)

### 激活函数MISH

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524152239.png)

### eliminate grid sensitivity

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524152333.png)

在σ(ty)前加上大于1的系数；

### 整体网络架构

![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image20220524152605.png)

