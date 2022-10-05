---
title: git的基本使用
tags: '-- git'
abbrlink: 29656
date: 2022-06-26 00:01:12
---

#### 1.删除仓库文件

先删除本地文件->git add -u

#### 2.创建test分支

列出所有分支git branch -a(带*绿色的为当前分支，白色和绿色的为当前分支，红色所有远端分支)->创建test分支git branch test->切换分支git checkout test->提交分支git push origin test

#### 3.把test分支合并到master分支

git merge test

#### 4.删除test分支

切换非删除的分支
git branch -D test 删除本地分支
git push --delete test 删除远端分支  删除远端分支时，本地分支不会被删除

#### 5.从github下载代码的时候一定要使用ssh地址，使用https地址的时候可能会出现问题

#### 6.从仓库拉去代码
git pull
#### 7.把代码推送到仓库
把文件添加到缓冲区 git add 文件名
把文件添加到本地仓库 git commit -a 本地提交的注释
把文件推送到仓库git push(origin 当前分支名)(亲测，如果是分支第一次提交不能省略，可能是因为要把新分支和代码同时推上去，否则括号内的内容可省)
#### 8.恢复被修改的文件
git checkout .(恢复被修改的所有文件)
git checkout -- 文件名/文件夹名(恢复被修改的文件名或则文件夹名)
#### 9.内容回滚
git reset HEAD^ 所有内容回退到上一个版本
git reset HEAD^ 文件名 具体文件回退到上一个版本
git reset 哈希值 回退到产生这个哈希值的状态
#### 10.如何拉取远端所有分支
get checkout -b 分支名  origin/分支名 切换到远端的分支并在本地命名

#### 这些平时就已经够用了，更加高级的用法用到时可自行百度
