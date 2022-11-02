---
title: torch.permute和torch.reshape的区别
tags:
  - torch函数
categories: 深度学习
abbrlink: 17446
date: 2022-11-02 13:13:49
---

# torch.permute

permute作用为调换Tensor的维度，参数为调换的维度。例如对于一个二维Tensor来说，调用tensor.permute(1,0)意为将1轴（列轴）与0轴（行轴）调换，相当于进行转置

# torch.reshape

reshape和view得到的tensor并不是转置的效果，而是相当于将原tensor的元素按行取出，然后按行放入到新形状的tensor中。

# torch.reshape和torch.view的区别

torch的view()与reshape()方法都可以用来重塑tensor的shape，区别就是使用的条件不一样。

view()方法只适用于满足连续性条件的tensor，并且该操作不会开辟新的内存空间，只是产生了对原存储空间的一个新别称和引用，返回值是视图。

reshape()即可以处理连续内存的数据，也可以处理不是连续内存空间的数据；当内存空间连续时和view()相同；当数据内存空间不连续时，就会对数据进行复制到连续内存空间上，然后再进行维度的改变。
