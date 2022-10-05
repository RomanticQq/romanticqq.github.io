---
title: hexo绑定域名
tags:
  - hexo
  - next
categories: hexo
abbrlink: 48994
date: 2021-01-05 20:08:28
---
1. **注册域名**
可以挑选[腾讯云](https://cloud.tencent.com/)或[阿里云](https://www.aliyun.com/)，或则其余任何一家进行域名注册

2. **获取github仓库IP**
打开`cmd`,`ping 仓库名.github.io`,获取IP
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105215709.png)
我的这个ping的有点问题，但方法没错
3. **域名和IP绑定**
找到控制台，点解析
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105220220.png)
然后点击修改，按照下面图片提示
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105220540.png)
4. **创建CNAME文件**
在`blog/source`目录创建`CNAME(无后缀名)`,把申请的域名填入即可
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105215242.png)
5. **域名和github仓库绑定**
打开存放博客的仓库，点击`settings`,找到
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105214939.png)
在输入框输入申请的域名，然后点击`save`
6. **访问**
域名，IP，https://仓库名.github.io，三则都可访问