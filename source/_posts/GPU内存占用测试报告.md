---
title: GPU内存占用测试报告
tags:
  - 深度学习
  - GPU
categories: 深度学习
abbrlink: 48938
date: 2022-08-26 09:00:28
---

**显卡：**NVIDIA GeForce GTX 1070

**batch-size：**4

**GPU内存：**8G

**模型：**resnet101

**数据集：**flower_data

**img.shpe:** (3, 512, 512)

# 测试情况

##### 默认(不使用混合精度、jit、tensorRT，函数：test_model)

| GPU内存占用 | 运行时间(s) |
| :---------: | :---------: |
|    6.6G     |     25s     |

##### 混合精度(只使用混合精度，函数：test_autocast_model)

| GPU内存占用 | 运行时间(s) |
| :---------: | :---------: |
|    4.2G     |     27s     |

##### jit(只使用jit，函数：test_jit_model)

| GPU内存占用 | 运行时间(s) |
| :---------: | :---------: |
|    2.0G     |     25s     |

##### jit+混合精度(test_antocast_jit_model)

| GPU内存占用 | 运行时间(s) |
| :---------: | :---------: |
|    2.0G     |     25s     |

##### tensorRT(只使用tensorRT，函数：test_trt_model)

| GPU内存占用 | 运行时间(s) |
| :---------: | :---------: |
|    3.3G     |     5s      |

##### 混合精度+tensorRT(函数：test_autocast_trt_model)

| GPU内存占用 | 运行时间(s) |
| :---------: | :---------: |
|    3.3G     |     5s      |

##### 

```python
def test_model():
    model = models.resnet101(pretrained=True).eval().to(device)
    for inputs, labels in tqdm(dataloaders['valid']):
        inputs = inputs.to(device)
        outputs = model(inputs)


def test_autocast_model():
    model = models.resnet101(pretrained=True).eval().to(device)
    with torch.autocast(device_type="cuda"):
        for inputs, labels in tqdm(dataloaders['valid']):
            inputs = inputs.to(device)
            outputs = model(inputs)


def test_jit_model():
    model = models.resnet101(pretrained=True).eval().to(device)
    model = torch.jit.script(model)
    model = torch.jit.freeze(model)
    for inputs, labels in tqdm(dataloaders['valid']):
        inputs = inputs.to(device)
        outputs = model(inputs)


def test_antocast_jit_model():
    model = models.resnet101(pretrained=True).eval().to(device)
    with torch.cuda.amp.autocast(cache_enabled=False):
        model = torch.jit.script(model)
    model = torch.jit.freeze(model)
    for inputs, labels in tqdm(dataloaders['valid']):
        inputs = inputs.to(device)
        outputs = model(inputs)


def test_trt_model():
    model = models.resnet101(pretrained=True).eval().to(device)
    x = torch.ones((1, 3, 512, 512)).cuda()
    model_trt = torch2trt(model, [x])
    model = TRTModule()
    model.load_state_dict(model_trt.state_dict())
    for inputs, labels in tqdm(dataloaders['valid']):
        inputs = inputs.to(device)
        outputs = model(inputs)


def test_autocast_trt_model():
    model = models.resnet101(pretrained=True).eval().to(device)
    x = torch.ones((1, 3, 512, 512)).cuda()
    model_trt = torch2trt(model, [x])
    model = TRTModule()
    model.load_state_dict(model_trt.state_dict())
    with torch.autocast(device_type="cuda"):
        for inputs, labels in tqdm(dataloaders['valid']):
            inputs = inputs.to(device)
            outputs = model(inputs)
```
