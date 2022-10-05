---
title: 解决createjs适配手机横屏的问题
tags:
  - 前端
  - createjs
categories: 前端
abbrlink: 12082
date: 2021-06-23 20:14:21
---
<!-- more --> 
当用createjs做手机游戏开发，通常会遇到游戏横屏的问题，此时难以开发，下面通过一些代码去解决这一问题。
<!-- more --> 
当开发时，可以通过谷歌浏览器打开手机横屏调试界面，进行页面的布局，并在布局前通过下面代码或得手机屏幕的宽高，然后进行适配:
```
//测试
// var gameScale = screenWidth/375;
// gameView.rotation = 90;
// gameView.x = screenWidth;
// gameView.y = 0;
// screenWidth = window.innerHeight;
// screenHeight = window.innerWidth;
//开发
screenWidth = window.innerWidth;
screenHeight = window.innerHeight;
```

当测试时，可以通过旋转屏幕的方式查看手机横屏后的效果：
```
//测试
 var gameScale = screenWidth/375;
 gameView.rotation = 90;
 gameView.x = screenWidth;
 gameView.y = 0;
 screenWidth = window.innerHeight;
 screenHeight = window.innerWidth;
//开发
//screenWidth = window.innerWidth;
//screenHeight = window.innerHeight;
```