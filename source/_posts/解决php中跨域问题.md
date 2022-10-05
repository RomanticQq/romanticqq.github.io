---
title: 解决php中跨域问题
tags:
  - php
categories: 后端
abbrlink: 60349
date: 2021-01-15 14:50:19
---
由于同源策略，经常会出现跨域问题，只需要在php代码前加上下面这些代码即可
```php
header("Access-Control-Allow-Origin:*");
header('Access-Control-Allow-Methods:POST');
header('Access-Control-Allow-Headers:x-requested-with, content-type');
```
