---
title: 详解TensorRT的C++/Python高性能部署
tags:
  - tensorRT
categories: 模型部署
abbrlink: 50203
date: 2023-03-07 14:25:36
---

# 学习内容

![image-20230307143026001](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071430197.png)

![image-20230307143104645](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071431782.png)

![image-20230307143616391](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071436555.png)

- 要实现高性能，对于预处理和后处理要写cuda核函数；

# 驾驭tensorRT的方案介绍

![image-20230307143935065](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071439333.png)

![image-20230307144103465](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071441650.png)

![image-20230307144215385](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071442521.png)

![image-20230307145015509](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071450648.png)

![image-20230307145149847](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071451065.png)

![image-20230307145550909](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071455060.png)

![image-20230307145737203](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071457434.png)

- torch2trt是由个人来维护的；
- 生成的trt engine是和设备绑定的，在一个型号的显卡上编译的模型不一定能在另一个显卡上好好的执行；
- 这种方法必须在设备上安装pytorch，然后再导出这个模型，因为从别的地方导出的模型是不一定能用的；

![image-20230307151111960](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071511112.png)

![image-20230307151648573](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071516697.png)

![image-20230307151917782](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071519984.png)

![image-20230307152326146](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071523248.png)

# 如何正确导出onnx并在C++中正确推理

![image-20230307153402167](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071534358.png)

![image-20230307153657443](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071536641.png)

![image-20230307153756859](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071537981.png)

![image-20230307154026675](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071540768.png)

![image-20230307154108420](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071541756.png)

![image-20230307154302209](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071543450.png)

![image-20230307155126651](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303071551724.png)
