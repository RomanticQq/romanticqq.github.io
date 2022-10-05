---
title: Python经典问题
tags:
  - Python
categories: Python
abbrlink: 59786
date: 2021-01-12 13:43:27
---
1. ### 交换两个变量的值
```Python
a=1
b=2
# 方法一:利用第三个变量实现
c=b
b=a
a=c

# 方法二:利用运算符实现
a=a+b
b=a-b
a=a-b

# 方法三:利用异或运算符实现
a=a^b
b=a^b
a=a^b
# 原理 a^b^b==a

# 方法四:使用Python特有的方法实现
a,b=b,a
```
2. for...in循环删除元素
