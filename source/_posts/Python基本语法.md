---
title: Python基本语法
tags:
  - Python
categories: Python
abbrlink: 24577
date: 2021-01-08 10:55:56
---
## Python基本语法
1. 注释
```python
# 单行注释
# ptint("Hello Python")  //用# 或ctrl+/
```
```python
# 多行注释
# print("你好")
# print("您好") //先选中，然后用Ctrl+/
```
2. 变量
```python
# 变量直接赋值
msg="abc"
``` 
3. input输入
```python
msg=input("请输入")
# msg为变量名
# input括号里为输入提示信息
```
4. del删除
```python
del(msg)
# msg：删除的变量名
```
5. 标识符规则
* 由字母，数字，下划线组成
* 开头不能是数字
* 不能是Python关键字
6. 数据类型
* str(字符串)
* Number(数字)
   - 整数
   - 浮点数
   - 复数`msg=1+2j`
* bool(布尔值)
* None(空值)
* list(列表)
* tuple(元组)
* dict(字典)
* set(集合)
```python
#使用type获取数据类型
msg=123
print(type(a))
```
7. 数据运算符的分类(与C语言一直的省略)
```python
# 求幂 **
print(2**3) # 2的3次幂
# 取整 //
print(12//5) # 12对5取整
```
8. 符合运算符(写法与C一致)
```python
a=a+b
等价于
a+=b
```
9. 关系运算符(与C一致)
```python
== != > < >= <=
```
10. 常用位运算符(将数字转化为二进制进行运算)
```python
& # 按位与
| # 按位或
^ # 按位异或
~ # 按位取反
<< # 左移位
>> # 右移位
```
11. print
```python
print(a,b,c); 
# 可以打印一个或多个变量或字符串
print(value1,value2,value3,,sep=' ',end='\n')
# sep值用来设定输出时多个值之间的连接符，默认是空格
# end值用来设定输出结束时的结束符，默认是换行
# sep,end两者都是以键值对的形式出现
```
12. input
```python
msg=input("提示信息") 
# input括号里保存的是提示信息
# 输入的信息会保存在变量msg
# 无论输入的是什么，msg的数据类型都为str
```