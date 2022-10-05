---
title: 搭建hexo个人博客
tags:
  - hexo
  - next
categories: hexo
abbrlink: 13713
date: 2021-01-03 15:37:20
---
## 准备工作
 1. 下载[node.js](https://nodejs.org/en/)
 2. 下载[git](https://git-scm.com/downloads)
 3. 配置环境变量
    1. 在node.js的安装目录下创建的创建两个文件夹，分别为node_global和node_cache
    2. 配置：此电脑/属性/高级系统设置/环境变量,先找到用户环境变量Path，然后点击编辑，新建，把node_global的绝对路径添加上去，确定
    3. 然后找到系统环境变量的Path,点击编辑、新建，把nodejs的安装目录的绝对路径添加上去 
 4. 更换node.js的源
    1. 设置淘宝镜像源
    `npm config set registry https://registry.npm.taobao.org`
    1. 查看使用的镜像源
    `npm config get registry`
    1. 安装淘宝镜像源
    `npm install -g cnpm --registry=https://registry.npm.taobao.org`
    **注**：可以更改也可以不更改，更换成国内的源后下载速度会变快，更改后以后执行npm命令要换成cnpm

## 在本地搭建hexo
 1. 在本地的任何一个磁盘创建一个文件夹blog(名字随意起)，为本地存储博客的文件夹
 2. 依次执行下列代码
 ```
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
   ```
3. 访问`http://localhost:4000`

## 选择自己喜欢的主题
1. 打开[hexo主题](https://hexo.io/themes/)官网，选择自己喜欢的主题下载
2. 下载完成后放在博客本地的文件夹里面，路径如：F:\blog\themes
3. 修改配置文件F:\blog\_config.yml
   搜索：**theme**关键字
   修改theme后的主题名，例如
   `theme: next`(切记：冒号和next之间有一个空格)
4. 再次访问`http://localhost:4000`，看主题是否发生了变化,若主题改变了则说明主题修改成功了。
5. 此时，博客本地搭建的已经成功了！
   



