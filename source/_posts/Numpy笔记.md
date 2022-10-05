---
title: Numpy笔记
tags:
  - 机器学习
categories: 机器学习
abbrlink: 31802
date: 2021-08-18 17:38:36
---

1. 两个数组相加

   ```python
   ya = np.array([1,2,3])
   b = np.array([1,2,3])
   c = a + b
   print(c)
   ```

2. 生成np数组

   ```python
   a = [1,2,3]
   b = np.array(a)
   print(b)
   ```

3. 生成矩阵

   ```python
   # 生成10*10 元素全为0的矩阵
   array_one = np.zeros([10,10])
   print(array_one)
   # 生成10*10 元素全为1的矩阵
   array_one = np.ones([10,10]) 
   print(array_one)
   # 只能生成0，1其余数字error
   ```

4. 生成数组

   ```python
   # 生成一个0～10，每次递增2的数组，不包括10
   a = np.arange(0,10,2)
   print(a)
   ```

5. 随机数组的创建

   ```python
   # 该函数可以保证生成的随机数具有可预测性，seed里的值相同，生成的随机数相同
   np.random.seed(10)
   # 均匀分布
   # 生成一个范围的整数
   a = np.random.randint(0,100)
   # 生成一个10*10且范围在0～1内的数
   b = np.random.rand(10,10)
   # 生成一个范围内的数
   c = np.random.uniform(0,100)
   # 正态分布
   ```

