---
title: Python字符串
tags:
  - Python
categories: Python
abbrlink: 35224
date: 2021-01-12 13:32:47
---
## 字符串
1. ### 单引号和双引号
```Python
在Python中可以使用一对单引号或双引号；也可以使用三对单引号或双引号
eg:
'hello'
"hello"
'''hello'''
"""hello"""

当字符串里面还有引号时，用单双引号嵌套使用，使表达的意思清晰
eg:
msg='xiaoming say"I am xiaoming"'
```
2. ### 字符串的转义字符\
```Python
# \' ==> 显示一个普通的单引号
# \" ==> 显示一个普通的双引号
# \n ==> 表示一个换行
# \t ==> 表示一个制表符
# \\ ==> 表示一个普通的\
# r'字符串' ==> 表示原生字符串，\n等会原生输出，不会表现特殊含义(r,R都可以)
eg:
x1='I\'m xiaoming'     # 若不用转移字符对'进行转义，则在m之前最会被截断，从而报错，不是一个字符串
x2='你好\n世界'     
# 打印是：
你好
世界
#中间会转行 
#若x3='你好\\n世界'
#打印结果是 你好\n世界     #因为已经对\进行转义，转义后仅表示一个普通的\字符 
m='hello\tworld'
n=r'hello\tworld'
print(m) # 打印 hello	world
print(n) # 打印 hello\tworld，因为r会使字符串保持原生
```
3. ### 字符串下标
```Python
# 下标又被称为索引，表示第几个数据
# str,list,tuple类型的数据可以通过下标获取或操作数据
# 切记，字符串是不可变数据类型(原数据永远不会修改，是在原数据的基础上新产生的数据)
# 下标是用0开始

# 可以通过下标来获取或则修改指定位置的数据
word='zhangsan'
print(word[4]) # 打印n

# 字符串是不可变数据类型
# 对于字符串的任何操作，都不会改变原有的字符串！！！
word='zhangsan'
# 不管对word做任何操作
print(word)   # word打印的结果恒为 zhangsan
```
4. ### 字符串切片
```Python
# 切片就是从字符串里复制一段指定的内容，生成一个新的字符串

# 切片语法
m[star:end:step]    # m是字符串的变量名
# 复制的内容中包含stat位，不包含end位
# step表示步长，每步取一个数据，step默认为1
m[Index] # 获取字符串指定下标的数据
m[star:end] # 获取从star到end的数据
m[star:] # 获取从star开始的所有数据
m[:end] # 获取从头开始到end的数据
m[::] # 从复制整个字符串
m[::step] #整个字符串每step复制一个数据
m[star:end:step] #获取从star到end,没step取一个数据

#注意
# 1.步长不能为0，但可以为负
# 2.当步长为负时，从star位开始向前运算
# 3.当step<0且star<end时，截取的内容为空(因为从star开始向前找不到end)
# 4.当star和end都为负数，表示从右向左数
```
5. ### 字符串常见操作
```Python
len(x) # 获取字符串长度

# 查找相关方法
x.find(a) # 查找字符串x中,字符c串a的下标，失败返回-1(返回a第一次出现的)
x.index(a)  # 查找字符串x中,字符串a的下标，失败会报错(返回a第一次出现的)
x.rfind(a)  # 查找字符串x中,字符串a的下标，失败返回-1(返回a最后一次出现的)
x.rindex(a)  # 查找字符串x中,字符串a的下标，失败会报错(返回a最后一次出现的)

# 判断相关方法
# is开头的都是判断结果是bool值
x.startswith(a) # 判断是否以字符串a开头
x.endswith(a) # 判断是否以字符串a结尾
x.isdigit() # 判断是否是纯数字
x.isalpha() # 判断是否是纯字母
x.isalnum() # 判断是否由纯字母数字组成(纯数字,纯字母,字母数字混合都为True,但当有其他字符如空格时就是False)
x.isspace() # 检测字符串是否只由空格组成,只有空格返回True,否则返回False

# 替换
x.replace(a,b) # 用b替换字符串x中的a    

# 分割
#按照指定字符串分割 
x.split(a) # 用字符串a将字符串x分割成一个列表
x.rsplit(a,b) # 用字符串a将字符串x从左切b次分割成一个列表
x.split(a) # 用字符串a将字符串x分割成一个列表
x.rsplit(a,b) # 用字符串a将字符串x从右切b次分割成一个列表
#按照行分割
x.splitlines() # 在有换行出\n处分割
#按照指定字符串分成三部分
x.partition(a) # 在第一个a处将字符串x分成三部分:a左侧,a,a右侧
x.rpartition(a) # 在最后一个a处将字符串x分成三部分:a左侧,a,a右侧
```
6. ### 修改大小写
```Python
x.capitalize() # 让字符串x第一个字符大写
x.upper() # 让字符串x中所有字符都大写
x.lower() # 让字符串x中所有字符都小写
x.title() # 让字符串x中所有单词首字母大写
```
7. ### 字符串填充
```Python
x.ljust(width) # 在字符串x的左边填空格，使字符串长度变为width(len(x)大于width，不做任何操作)
x.rjust(width) # 在字符串x的右边填空格，使字符串长度变为width(len(x)大于width，不做任何操作)
x.center(width) # 在字符串两侧平均填空格，使字符串长度变为width(len(x)大于width，不做任何操作)
x.ljust(width,fillchar) # 在字符串x的左边填filechar，使字符串长度变为width(len(x)大于width，不做任何操作)
x.rjust(width,fillchar) # 在字符串x的右边填filechar，使字符串长度变为width(len(x)大于width，不做任何操作)
x.center(width,fillchar) # 在字符串两侧平均填fillchar，使字符串长度变为width(len(x)大于width，不做任何操作)
```
8. ### 增删空格
```Python
x.lstrip() #去除x中左侧的空格
x.rstrip() #去除x中右侧的空格
x.lstrip(chars) #去除x中左侧的chars
x.rstrip(chars) #去除x中右侧的chars
```
9. ### 列表、字符串之间的转化
```Python
x.split(str) # 用字符str把x分成一个list
str.join(chars) # 用字符str把chars连接成一个字符串
# chars是一个可迭代的对象
```
10. ### 字符串的运算符
```Python
# 1.字符串和字符串之间可以相加
# 2.字符串和数字之间可以相乘
# 3.字符串和数字之前：==为False；!=为True
# 4.字符串和字符串之间做比较运算，会逐个比较字符串的编码值
# 5.不支持其他运算符
```
11. ### 利用内置函数实现数字、字符间的转化(ASCII码)
```Python
ord(char) # 查看字符char的ASCII码
chr(num) # 查看ASCII码num所对应的字符
```
12. ### in 和 not in
```Python
in # 用来判断一个内容是否在可迭代对象中
not in # 用来判断一个内容是否不在可迭代对象中
```
13. ### 使用% 占位符来格式化字符串 
```Python
# %s    表示的是字符串的占位符
# %d    表示的整数的占位符
# %nd   打印时显示n位，如果不够，n>0在前面用空格补齐,n<0在后面补空格
# %0d   打印时显示n位，如果不够，在前面用0补齐
# %f    表示浮点数的占位符
# %nf   表示浮点数的占位符,四舍五入保留n为小数
# %%    打印一个%
# %x    将数字按16进制输出，字符为小写
# %X    将数字按16进制输出，字符为大写
# print('%3d'% 15) ##语法
```
14. ### format方法 
```Python
# {} 可以用来占位，用format中的数据进行填充

# 一一对应填充
# x='大家好,我是{},今年{}岁'.format('xiaoming',18)

# {数字}，数字从0开始
# x='大家好,我是{1},今年{0}岁'.format(18,'xiaoming')

# {变量名},相当于键值对
# x='大家好,我是{name},今年{age}岁'.format(name='xiaoming',age=18)

# {数字}{变量名}混合使用
# x='大家好,我是{name},今年{1}岁,身高{0}cm'.format(180,18,name='xiaoming')
# 要先写数字的值，再写变量名的值

# 用list填充
# data=['xiaoming',18,180]
# x='大家好,我是{},今年{}岁,身高{}cm'.format(*data)
# 切记加*

# 用dictionary填充
# data={'name':'xiaoming','age':18,'high':180}
# x='大家好,我是{name},今年{age}岁,身高{high}cm'.format(**data)
# 切记加**
```
