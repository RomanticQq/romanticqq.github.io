---
title: Python分支语句和循环语句
tags:
  - Python
categories: Python
abbrlink: 49927
date: 2021-01-10 10:54:42
---
## 分支语句
1. ### if
```Python
if 判断条件:
    条件成立时，执行的语句
eg:
if 1 < 2 :
    print("helloworld")
```
2. ### if...else
```Python
if 判断条件:
    条件成立时，执行的语句
else
    当if中的条件不成立时，执行的语句
eg:
msg=1
if msg==0 :
    print("helloworld")
else:
    print("你好")
eg:
if 1 < 2 :
    print("helloworld")
```
3. ### if...elif...else
```Python
if 条件1:
    条件1成立，执行语句
elif 条件2:
    条件2成立，执行语句
else:
    当所有条件都不成立时，执行的语句
eg:
msg=10
if 0 <msg<3 :
    print("helloworld")
elif 3<= msg <=10 :  #在Python中，允许这样进行左右判断
    print("你好")
else:
    print(msg)
```

4. pass关键字
```Python
# pass关键字在Python中没有意思，只是用来占位，保证代码的完整性
eg:
if 1 < 2 :
    pass   # pass无意义，保证代码完整性
```
5. ### if语句注意点
```Python
1.区间判断
在Python中可以进行连写判断,如 0<=msg<=10
2.隐式类型转换
if后面需要一个bool类型的值，若不是bool类型的值，则会自动转换
eg：
if 1 :
    print("你好") # 1会自动转换成bool类型的值true
3.三元表达式(对if...else的简写)
x=num1 if num1 > num2 else num2
eg:
x=1 if 1 < 2 else 2 
print(x)   # 打印出的结果为1
4. 在Python中不支持switch...case...
5. 在Python中使用强制缩进来表示语句之间的结构
```

## 循环语句
1. ### while循环
```Python
while 判断条件:
    条件成立时,执行的语句
eg:
while 2<3:
    print("hello world")
```
2. ### for循环
```Python
for ele in iterable:
    执行语句
#这个和别的语言有所区别,对于计算数的时候一般用range
for i in range(0,5):
    print(i) # 打印结果为0,1,2,3,4
```
3. ### for...in循环
```Python
# for...in循环的本质是不断的调用next方法查找下一个数据
for ele in iterable:
    执行语句
eg:
for i in range(1,5):
    print("aaa")
```
4. ### for...else循环
```Python
for ele in iterable:
    执行语句
    if 条件判断:
        break   # 若break被执行，则退出for...each循环，each不会被执行
else:
    执行语句 # 当for语句执行完后且没有被break,则最后再执行each语句
eg:
for i in range(1,5):
    print("aaa")
    if i==3:
        break
else:   # 当for里面break被执行，each就不会被执行
    print("111")
```
5. ### break和continue
```Python
break:终止本层循环
continue:终止本次循环
```
6. ### 循环语句注意事项
```Python
1. Python中没有i++或i--,只能i+=1
2. 常用range内置类生成一个整数区间进行循环
3. range生成的整数区间以前一个数开始，以后一个数的前一个整数结束
4. in后面是一个可迭代的对象,目前接触到的接迭代的对象:字符串,列表,字典,元组,集合,range
5. Python中没有do...while...
```

