---
title: 学习Python遇到的坑(更新中)
tags:
  - Python
categories: Python
abbrlink: 4895
date: 2021-01-08 12:55:56
---
1. ### 在cmd中输入Python打开软件商店
&nbsp;&nbsp;&nbsp;&nbsp;原因：在系统环境变量和用户环境变量的`path`中，当`WindowsApps`在`python`所配置的环境变量前的时候，就会先打开`WindowsApps`
&nbsp;&nbsp;&nbsp;&nbsp;解决方法：1.在系统环境和用户环境变量的`path`中删掉`WindowsApps`这一项；2.在系统环境和用户环境变量的`path`中将`WindowsApps`这一项移动到`python`环境变量的下面，这样`python`环境变量就会先被执行，不会造成那样的意外
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210108143304.png)