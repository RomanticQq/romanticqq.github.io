---
title: swim transformer的理解
tags:
  - transformer
categories: 计算机视觉
abbrlink: 47606
date: 2023-03-16 14:43:04
---

[参考博客](https://blog.csdn.net/qq_37541097/article/details/121119988)

[参考视频](https://www.bilibili.com/video/BV1pL4y1v7jC/?spm_id_from=333.788&vd_source=0a0fc78c4f646862160e365c9909f8f7)

![image-20230316150350681](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303161503723.png)

![2](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/202303161450636.png)

1. 在`Patch Partition`中，对于图片的下采样不是采用卷积的形式，而是采用真正分割的方式；
2. 在进行注意力计算时，token的长度和通道数相等，比如[h,w,c]，那么就有h*w个token；
3. 添加偏置项是在Q*K之后进行的；
4. SW-MSA中的mask是在添加完偏置项以后加上去的，W-MSA省略这一步；
5. 每个stage只创建一次mask，因此尺寸大小相等，不用重复创建；
