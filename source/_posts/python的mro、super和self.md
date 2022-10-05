---
title: python的mro、super和self
tags:
  - Python
categories: Python
abbrlink: 48741
date: 2022-06-13 11:05:47
---

### mro

**mro是每一个类会把它所有的父类和自己做一个线性化serialization，也就是把所有的继承类和自己做一个排队，这个排队要保证自己是最高优先级。**

```python
# 定义两个父类
class A:
    def say(self):
        print("A")
        
        
class B:
    def say(self):
        print("B")
```

```python
# 情况1
class M(A, B):
    pass


m = M()
m.say() # A
# 此处M.mro()是M,A,B(因为在继承的时候A在前，所以A的优先级高于B)
# 因为m调用了say函数，会按照m所在类的mro的顺序从前到后在类里找say函数,先在类A里找到了，因此输出为A
```

```python
# 情况2
class C(A):
    pass


class M(C,B):
    pass


m = M()
m.say() # A
# 此处M.mro()是M,C,A,B(因为在M继承C和B的时候先继承的C,所以C及C的父类的优先级都高于B)
# 因为m调用了say函数，会按照m所在类的mro的顺序从前到后在类里找say函数,先在类A里找到了，因此输出为A
```

```python
# 情况3
class C(A):
    pass


class D(A):
    def say(self):
        print("D")


class M(C,D):
    pass


m = M()
m.say() # D
# 此处M.mro()是M,C,D,A
# 因为M继承了C,D   C继承了A  D继承了A
# C,D都继承了A,那么A的优先级以A最后出现的位置为准
# 因此M,C,D,A先在D中找到了say函数
# 这可能有一个疑问：为什么C已经继承A了，那么C中不是应该有A中的say函数吗？为什么不是输出A？
# 在这里只有找到了类里真真正正存在的该函数才可以，继承关系是不可以的
```

```python
# 情况4
class C(A, B):
    pass


class D(B, A):
    pass


class M(C, D):
    pass

# 这样的写法是会报错的，因为当继承相同的父类时，顺序一定要相同
```

总结：

1. 每个类只会按排列好的类的优先级去执行自己类里面的函数，若B继承A，B里面没有say函数而A里面有，那么即使B的优先级高，B也不能执行say函数，只能优先级到A时，自己调用自己类里的say函数；
2. 当存在多继承时，在当前类的继承关系中先出现的类的优先级高（情况1）；
3. 当存在A被多个类继承时，A的优先级由最后一次出现的位置决定（情况3）；



### super

```python
super(class, object/class).__init__([参数])
# 参数1：决定了在mro链上从哪个类的下一个开始查找__init__函数
# 参数2：决定了这一个函数bind到哪一个object或则class上，同时决定了使用哪一个mro
# 参数3：需给找到的__init__传的参数
# 参数1和参数2有时候是可以省略的，当省略时，参数1为当前的类名，参数2为该所在函数第一个参数
```

```python
class A:
    def __init__(self, name):
        self.name = name


class B(A):
    def __init__(self, name, age):
        self.age = age
        super(B, self).__init__(name)


c = B('xiaoming',16)
print(c.name)
print(c.age)
# 在类B中，super(B, self).__init__(name)和super().__init__(name)的作用是相同的
# super的执行流程(以本段代码中的super为例)：首先它要从self这个object中拿到mro，然后
#从类B的后一个class开始查找__init__函数，当找到__init__函数后进行赋值，然后再把__init__函数bind到
#self上；在这个例子中，先通过self拿到mro(B,A)，然后从B后面的类开始查找，即A类中有__init__函数，然后
#对__init__函数中的name进行赋值，并返回给self
```



### self

[在类内用类名和self的区别](https://www.cnblogs.com/nemolmt/p/6646764.html)

