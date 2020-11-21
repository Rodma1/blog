---
title: python学习第四天——函数类型（变量，引用，匿名，递归）
tags:
  - python
categories:
  - python基础
abbrlink: 14557
date: 2020-10-31 14:09:11
---



前言

> 这是我听老师讲课做的笔记,考试要看的。 
>
> 作者：RodmaChen 
>
> 关注我的[csdn博客](https://blog.csdn.net/weixin_46654114)，更多数据结构与算法知识还在更新



## 一. 局部和全局变量

```python
# 局部变量 就是在函数内部定义的变量【作用域仅仅局限在函数的内部】
# 不同的函数 可以定义相同的局部变量，但是各自用各自的 不会产生影响
# 局部变量的作用：为了临时的保存数据 需要在函数中定义来进行存储
# ------------全局变量----------------
# pro的定义就是一个全局变量【作用域的范围不同】
# 当全局变量和局部变量出现重复定义的时候，程序会优先执行使用函数内部定义的变量【地头蛇】
#如果在函数的内部要想对全局变量进行修改的话 必须使用global 关键字进行声明
# 对于可变类型【dict、list】来讲，全局变量要想在函数中修改的话，我们不需要用global关键字去声明的
# 【因为对象的内存地址不会改变】
c=3#c为全局变量，可以被所有函数调用
a=2
def Test():
    b=2#b为局部变量，只能在函数内被调用
    global a#局部变量变为全局变量
    a=4
    print('{}'.format(a))
    pass
def Test2():
    c=4
    print('{}'.format(c))
    pass
Test2()
print(c)#c没有发生改变说明全局变量在函数中无法修改
Test()
print(a)#a发生了改变说明声明全局变量 后才可以修改

# 可变类型列表，字典 dict list，可以在函数中修改
listA=[]
print(type(listA))
def demoList():
    listA.append('python')#向空列表里面添加数据
    pass
demoList()
print(listA)#发现输出数据了

# 不可变类型str tuple number【int、float、complex】
```



## 二. 引用

```python
#在python中，值是靠引用来传递来的，可以用id()查看一个对象的引用是否相同，id是值保存在内存中那块内存地址的标识。

# 可变类型 列表和字典：函数调用全局变量后地址不会变化
li=[]
print('原来的地址{}'.format(id(li)))
def Test(n):
    li.append([1,3,'chen'])
    print(id(n))
    print('内部的{}'.format(n))
    pass
print(id(li))
Test(li)#输出我们发现地址是一样的
print('外部的变量对象{}'.format(li))

#不可变类型
a=1
def func(x):
    print('x刚开始的地址{}'.format(id(x)))
    x=2
    print('x的值修改之后地址{}'.format(id(x)))#改变类型后地址发生了变化
    print(x)
    pass
#调用函数
print('a的地址:{}'.format(id(a)))
func(a)
print(a)
```



## 三. 匿名

```python
# 1.使用lambda关键字去创建函数
# 2.没有名字的函数
# 3.匿名函数冒号后面的表达式有且只有一个, 注意：是表达式，而不是语句
# 4.匿名函数自带return，而这个return的结果就是表达式计算后的结果
# 缺点
# lambde只能是单个表达式，不是一个代码块，lambde的设计就是为了满足简单函数的场景，
# 仅仅能封装有限的逻辑,复杂逻辑实现不了，必须使用def来处理

M=lambda x,y:x+y
print(M(2,3))#M相当于一个调用函数
#可以使用if-else语句,三元运算

Test=lambda x,y:x if x>y else y#意思就是调用x和y两个变量，如果x大于y就取x否则取y
print(Test(2,3))

# 也可以单个参数使用
Test=lambda x:(x**2)
print(Test(10))
```



## 四. 递归



```python
#说难不难，有点绕，就是自己调用自己
# 递归满足的条件
# 自己调用自己
# 必须有一个明确的结束条件
# 优点：逻辑简单、定义简单
# 缺点：容易导致栈溢出，内存资源紧张，甚至内存泄漏
# 求阶乘
# 循环的方式去实现
#下列是求阶乘
# 循环的方式去实现
def jiecheng(n):
    result=1
    for item in range(1,n+1):# range左闭右开，所以要加一
        result*=item
        pass
    return result
print(jiecheng(5))
# 递归的方式实现
def factorial (n):
    if n == 1:
        return 1
    return n * factorial (n-1)
print(factorial(5))
```

> 本人博客：[https://blog.csdn.net/weixin_46654114](https://blog.csdn.net/weixin_46654114)
> 本人b站求关注：[https://space.bilibili.com/391105864](https://space.bilibili.com/391105864)
> 转载说明：跟我说明，务必注明来源，附带本人博客连接。

请给我点个赞鼓励我吧
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507113619405.png#pic_center)