---
title: hexo+PicGo+gitee图床
tags:
  - hexo
  - PicGo
  - gitee
  - Typora
  - 图床
categories: hexo
abbrlink: 13481
date: 2021-01-05 19:26:41
---
**前言**：我尝试了好几种床图，不是在电脑端加载不出来，就是有各种各样的限制，最后找到了gitee，因为服务器在国内，访问速度也是比较快，空间也没有限制，算是比较理想的一种吧。一开始我用vscode+PicGo插件，等到快成的时候，图片是上传上去了，但是加载不出来，我尝试了`sm.ms`和`github`，最后抛弃了`vsCode+PicGo`插件，选择了`PicGo客户端和gitee`。

1. **注册gitee账号**
去官网注册账号[gitee](https://gitee.com/)
2. **新建gitee仓库**
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105203048.png)
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105203450.png)
3. **获得gitee的token**
登录`gitee`官网，点击头像/设置/私人令牌/生成令牌
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105203902.png)
点击提交后复制生成的令牌，在配置的时候要使用
4. **下载gitee**
点击[PicGo](https://github.com/Molunerfinn/PicGo/releases)下载，有不同的版本，都可以
下载成功后按照提示默认安装即可
5. **配置gitee**
默认状态下PicGo是没有`gitee`，因此先安装插件`gitee-uploader`
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105205151.png)
这时，点击图床设置，已经有`gitee图床`的设置
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105205522.png)
    ```
    1:打开新建的仓库，看地址栏，若地址栏为https://gitee.com/A/B,则需要填A/B
    2:默认为master就可以
    3:把刚才生成的token粘贴到这里
    4:path为创建的仓库存放图片的文件夹名，可以为image，可任意填写
    5:其余开心就好
    ```
6. **升华**
为更方便地获取截图外链，安装`picgo-plugin-quick-capture`,实现截图上传一步搞定
7. **Typora+PicGo+gitee配置**
如果用`Typora`写`Markdown`文章，还需要对`Typora`进行配置，找到`文件/偏好设置/图像`
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105212825.png)
在typora中，当插入本地图片时，会自动转换成gitee外链

**tips**
1. 通过上面的操作已经实现了快速上传和快速截图上传功能，当我们要用本地图片生成外链时，先复制一下本地图片(就是选中图片按下Ctrl+c),然后按下快速上传的快捷键，此时外链已经生成，在需要插入图片的位置Ctrl+V就可以了
2. 当使用快速截图上传时，如果是直接截图的话，截完图后直接Ctrl+V就可以了，但如果是截完图后需要写批注，那么截的图并不一定可以自动上传，需要按下快速上传的快捷键，然后再Ctrl+V
3. 通过PicGo可以查看和删除上传的图片
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105212411.png)
