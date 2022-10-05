---
title: 解决Pytorch-CIFAR-10数据集下载问题
tags:
  - pytorch
  - CIFAR10
  - 深度学习
categories: Pytorch
abbrlink: 20203
date: 2021-10-14 18:26:18
---

### 问题

错误：[Errno socket error] [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed。

### 解决方案

全局取消证书验证（当项目对安全性问题不太重视时，推荐使用，可以全局取消证书的验证，简易方便）

```python
import ssl
ssl._create_default_https_context = ssl._create_unverified_context
```