---
layout: pytorch
title: nn.DataParallel的坑
date: 2022-11-10 09:35:45
tags:
  - pytorch
categories: pytorch
---

nn.DataParallel是pytorch使用多gpu训练时所使用的方法，但是使用nn.DataParallel之后，模型的读取就会有所不同。

### 当训练时没有使用nn.DataParallel，而测试时使用

这种情况就会报错，应该先把模型加载进来，在使用nn.DataParallel

```python
model.load_state_dict(torch.load(save_path))
model = nn.DataParallel(model, device_ids=[0, 1]) 
```



**造成这些问题的根本原因是因为模型经过nn.DataParallel后，权重参数的形式会发生变化**

```python
module.features.0.weight # 经过nn.DataParallel
features.0.weight # 没有经过nn.DataParallel
# 没有经过nn.DataParallel的模型，没有model.module这个属性
# 经过nn.DataParallel的模型，给模型传参时使用model.module(params)，比如给forward传数据时
```



