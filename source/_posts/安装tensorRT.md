---
title: 安装tensorRT
tags:
  - tensorRT
categories: 工具
abbrlink: 54278
date: 2022-11-01 09:45:24
---

1. 下载cuda、cudnn、tensorrt；
2. 把cudnn下的lib、bin、include对应复制到cudn下面；
3. 把tensorrt的lib加到环境变量中；
4. 安装pycuda时去官网下载whl文件，直接装可能会报错；如果cuda版本太高，用pycuda最新的版本就可以，不用回退cuda版本；
5. 安装下载好的tensorrt；
