---
layout: python
title: numpy.transpose手算
date: 2021-10-26 17:30:18
tags:
	- numpy
categories: numpy
---

原理解析请看：[点击1](https://blog.csdn.net/u012762410/article/details/78912667) [点击2](https://www.freesion.com/article/149821286/)

##### 当是二维时

直接对矩阵进行转置；

```python
array([[0, 1],
       [2, 3]])

transpose后

array([[0, 2],
       [1, 3]])
```

##### 当是三维时

交换x,y时：

```python
A = array([[[ 0,  1,  2,  3],
            [ 4,  5,  6,  7]],
            
           [[ 8,  9, 10, 11],
            [12, 13, 14, 15]]])
            
transpose后

A = array([[[ 0  1  2  3],
  [ 8  9 10 11]],

 [[ 4  5  6  7],
  [12 13 14 15]]])
# 可以直接把三维数组看成二维数组，把一个一维数组看成一个数，继续使用二维数组转置的方式即可；
```

np.transpose(img, (1, 0, 2))操作，可以将图像逆时针翻转90度

