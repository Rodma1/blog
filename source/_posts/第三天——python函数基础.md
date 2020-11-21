---
title: python学习第三天——函数基础练习题
tags:
  - python
categories:
  - python基础
abbrlink: 10465
date: 2020-10-31 13:57:35
---



前言

> 这是我听老师讲课做的笔记,考试要看的。 
>
> 作者：RodmaChen 
>
> 关注我的[csdn博客](https://blog.csdn.net/weixin_46654114)，更多数据结构与算法知识还在更新

附加知识点

> 1. **不定长参数**：一个函数有时候会处理比当初声明的参数要多，这就是不定长参数，定义函数时不用声明参数名。加了星号（*）的变量args会存放所有未命名的变量参数，args为元组；而加**的变量kwargs会存放命名参数，即形如key=value的参数， kwargs为字典。
> 2. **缺省参数**： 缺省参数，在调用函数时如果没有传参数，那么会使用定义函数时给的缺省值。缺省参数必须在参数列表的最后面，否则会报错
> 3. **引用传参**： Python中函数参数是引用传递（注意不是值传递）。对于不可变类型，因变量不能修改，所以运算不会影响到变量自身；而对于可变类型来说，函数体中的运算有可能会更改传入的参数变量。

####  写函数，接收n个数字，

```python

# 可以用元组
def sum(*args):
    result=0
    for item in args:
        result+=item
        pass
    return result
    pass

print(sum(1,2,3,4,5))
```

#### 写函数，找出传入的列表或元组的奇数位对应的元素，并返回一个新的列表

```python


def list_tuple(args):
    '''
    处理列表数据
    :param con: 接受的是一个列表或者元组
    :return: 新的列表对象
    '''
    listA=[]#定义一个空列表，待会往里面存入奇数
    for item in args:
        if(item%2!=0):
            listA.append(item)#追加进去
            pass
        pass
    return listA
    pass
print(list_tuple([1,2,3,4,5,6]))
a=tuple(list_tuple([1,2,3,4,5,6]))

print(a)
print(type(a))

```



##### 写函数，检查传入字典的每一个value的长度,如果大于2，那么仅保留前两个长度的内容，并将新内容返回给调用者。

```python
# PS:字典中的value只能是字符串或列表

def _dict(**args):
    _NULL={}#定义一个空字典
    for key,value in args.items():#获取所有键和值
        if len(value)>2:#如果值的长度大于2
            _NULL[key]=value[:2]#_NULL存取args的键值和值的前两个字符
            pass
        else:
            _NULL[key]=value#小于二直接返回
            pass
        pass
    return _NULL
    pass
dictObj={'name':'夏雨','hobby':['唱歌','跳舞','运动','编程'],'pro':'中国艺术'}
print(_dict(**dictObj))
# 本题做错点： for循环要获取键和值，value[:2]学成了args[:2]. =value学成了args[value]
```

> 本人博客：[https://blog.csdn.net/weixin_46654114](https://blog.csdn.net/weixin_46654114)
> 本人b站求关注：[https://space.bilibili.com/391105864](https://space.bilibili.com/391105864)
> 转载说明：跟我说明，务必注明来源，附带本人博客连接。

请给我点个赞鼓励我吧
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507113619405.png#pic_center)