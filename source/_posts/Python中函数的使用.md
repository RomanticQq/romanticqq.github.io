---
title: Python中函数的使用
tags:
  - Python
categories: Python
abbrlink: 51896
date: 2021-01-11 23:30:09
---
1. 函数定义语法
```Python
# def 函数名(参数):
#    函数要执行的语句
eg:
def say(person):
    print('{}说：他明天去旅游'.format(person))
```
2. 传参
```Python
# 1.一一对应传参
say('xiaoming')
# 2.通过变量名给形参赋值
say(person='xiaoming')
```
3. 返回值
```Python
1. return a #语法
2. 通常情况下只能return一次
3. 如果一个函数没有返回值，那么它的返回值就是None
4. 在特殊情况下(finally语句)，一个函数可能会执行多个return语句
```
4. 函数的注释
```Python
在定义函数名的下一行按三对双引号，然后回车
"""

:param person:
:return:
"""
```
5. 全局变量和局部变量
```Python
1. 定义在函数外的为全局变量
2. 定义在函数内的为局部变量
3. 如果局部变量和全局变量重名时，会在函数内部又定义一个新的局部变量，而不是修改变全局变量
4.如果在函数内部想要修改全局变量，则用global
eg：想要在函数内部修改全局变量name
global name
name='xiaoming'
5.使用内置函数查看全局变量和局部变量
globals() # 查看当前.py中的全局变量
locals()  # 查看当前.py中的局部变量
6. 在Python中只有函数分作用域
```
6. 函数多个返回值
```Python
1. 函数返回多个结果，就是将多个数据打包成一个整体返回，可以使用列表和字典
2. 通常情况下使用元组
3. 接受多个返回值时，若一直返回值个数，可直接用变量分别接受
eg:
def test():
    return 1,2
x,y=test()
print('x={},y={}'.format(x,y))
```
7. 缺省参数
```Python
定义：有些函数的参数是有默认参数，你传了用你的，不传用默认的
eg:
def say(person='xiaoming'):
    print('{}说：他明天去旅游'.format(person))

say() # 当say函数不传参数时，就使用默认参数
```
8. 特殊传参
```Python
1. 当位置参数和关键字参数混合使用时，位置参数在前
eg:
say('xiaoming',age=18)  # 位置参数前，关键字参数后

2. 位置可变参数
def say(name,*args):
    pass

say('xiaoming')  # args为空
say('xiaoming',18)  # 18以元组的形式存在args里
# 多出来的可变参数会以元组的形式保存在args里
# 在定义函数参数时,先写位置参数再写可变位置参数，传参时也是
# 注意是一个*

3.可变关键字参数
def say(name,**kwargs):
    pass

say(name='xiaoming')  # kwargs为空
say('xiaoming',18)  # 18以元组的形式存在kwargs里
# 多出来的可变参数会以字典的形式保存在kwargs里
# 在定义函数参数时,先写位置参数再写可变位置参数，传参时也是
# 注意是**

4.当位置参数，可变位置参数，缺省参数，关键字参数，可变关键字参数同时出现时
def say(位置参数，可变位置参数，缺省参数，关键字参数，可变关键字参数)  
#传参时也是一样
```
9. 注意事项 
```Python
1. 在Python中函数不允许重名,重名后一个会覆盖前一个
2. 函数名和变量名也不能重名
```