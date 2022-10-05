---
title: small tips
tags:
  - 深度学习
categories: 深度学习
top: 2
abbrlink: 64603
date: 2022-08-26 09:07:52
---

1. 在pytorch中，如果用交叉熵损失，则模型的最后一层不能是`nn.Softmax()`，因为在交叉熵损失中已经内置了`nn.Softmax()`，用两次会造成损失收敛缓慢甚至不收敛；
1. 给文件起名字的时候不要与安装的包的名字相同，否则导包时可以会导本地同名的文件，调用包里的方法就会报，没有发现该模块；
1. 安装完augly，发现导包失败，`pip uninstall python-magic; pip install python-magic-bin==0.4.14`；
1. 训练vgg16时，学习率不能设置太大，比如设置为0.001时，就会造成损失函数不下降，模型不收敛，可以设置为0.0001；
