---
title: C语言函数数组传值
tags:
  - C语言
categories: C语言
abbrlink: 35573
date: 2021-01-13 23:02:01
---
C语言中,向函数传值的问题
```C
// 方法一
#include<stdio.h>
int duplicate(int* number);
int main(){
	int number[5]={1,2,3,4,5};
	duplicate(number);
	return 0;
}
int duplicate(int *number)
{
	printf("%d",number[0]);
}
//方法二
#include<stdio.h>
int duplicate(int number[]);
int main(){
	int number[5]={1,2,3,4,5};
	duplicate(number);
	return 0;
}
int duplicate(int number[])
{
	printf("%d",number[0]);
}
```