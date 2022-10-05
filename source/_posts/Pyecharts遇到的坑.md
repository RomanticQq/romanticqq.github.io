---
title: Pyecharts遇到的坑
tags:
  - 机器学习
categories: 机器学习
abbrlink: 10521
date: 2021-01-18 15:33:01
---
因为Pyecharts高版本不兼容低版本的问题，相同的语法在不同的版本就可能会出现一个能正常运行而一个出现报错的情况
常见的有导包时就有可能出现错误
```python
from pyecharts.charts import Bar,Pie,Line # 1.x版本的语法
from pyecharts import Bar,Pie,Line # 0.5.x版本的语法

#若交换使用就会报错 
```
还有
```python
bar_1 = Bar("每天被领劵的数量",width=1500,height=600)

# 在0.5.x版本下就是正确的，在1.x版本下就是错误的
```
在用`pip`命令安装时默认安装的是高版本，下面是卸载`Pyecharts`的命令和安装低版本的命令
```python
pip install pyecharts # 默认安装高版本
pip uninstall pyecharts # 卸载pycharts(无论任何版本)
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pyecharts==0.5.5 # 安装0.5.5
```
