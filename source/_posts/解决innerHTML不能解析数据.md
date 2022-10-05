---
title: 解决innerHTML不能解析数据
tags:
  - 前端
categories: 前端
abbrlink: 31746
date: 2021-01-15 15:25:23
---
当使用`document.('div').innerHTML=`` `向页面追加内容时可能会出现变量不解析的情况。
正确姿势：`=`后面是` `` `,而不是单引号或双引号,只有` `` `才能解析。
```html
document.querySelector('div').innerHTML=`<h2>编号：${resp.id}</h2>`	
```