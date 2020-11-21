---
title: 第六天——python面向对象基础之魔术方法
tags:
  - python
categories:
  - python基础
abbrlink: 58275
date: 2020-10-31 15:05:12
---



前言

> 这是我听老师讲课做的笔记,考试要看的。 
>
> 作者：RodmaChen 
>
> 关注我的[csdn博客](https://blog.csdn.net/weixin_46654114)，更多数据结构与算法知识还在更新

##  一. 类和对象

通俗理解：类就是模板，对象就是通过模板创造出来的物体



类(Class)由3个部分构成：

类的名称: 类名 

类的属性: 一组数据 

类的方法: 允许对进行操作的方法 (行为)



## 二. 魔法方法



在python中，有一些内置好的特定的方法，方法名是“__xxx__”,在进行特定的操作时会自动被调用，这些方法称之为魔法方法。
下面介绍几种常见的魔法方法。

```
__init__方法：初始化一个类，在创建实例对象为其赋值时使用。
__str__方法：在将对象转换成字符串  str(对象)  测试的时候，打印对象的信息。
__new__方法：创建并返回一个实例对象，调用了一次，就会得到一个对象。
__class__方法：获得已知对象的类 ( 对象.__class__)。
__del__方法：对象在程序运行结束后进行对象销毁的时候调用这个方法，来释放资源。
……
```



## 三. 理解self

> self和对象指向同一个内存地址，可以认为self就是对象的引用。



```python
# 创建一个类 
class Car(object): 
 	# 创建一个方法打印 self 的id 
 	def getself(self): 
 		print('self=%s'%(id(self))) 
 
bmw = Car() 
print(id(bmw))
bmw.getself() 
'''输出
140033867265696 
140033867265696 
'''
```

> 所谓的self，可以理解为对象自己，某个对象调用其方法时，python解释器会把这个对象作为第一个参数传递给self，所以开发者只需要传递后面的参数即可。

```python
# 创建一个类 
class Car(object): 
	def __init__(self,name,colour): 
		self.name = name 
		self.colour = colour 
	# 创建一个方法打印 self 的id 
	def getself(self): 
		print('self=%s'%(id(self))) 

bmw = Car('宝马','黑色') 
# 实例化对象时，self不需要开发者传参，python自动将对象传递给self 
print(id(bmw)) 
bmw.getself() 
```



## 三. 练习对战



> 做两个人物对战

```python
import random
import time
#定义类
class hero(object):
    # 定义属性
    def __init__(self,name,blood,dblood,ablood):
        self.name=name#名字
        self.blood=blood#血量
        self.dblood=dblood#这是减少的血量
        self.ablood=ablood
    #定义方法
    # 互捅
    def tong(self,enemy):
        enemy.blood-=self.dblood
        print('%s砍掉了%s%d的血量'%(self.name,enemy.name,self.dblood))

    def addblood(self):
        self.blood+=self.ablood
        print('%s吃了一颗补血药，加了%d血量'%(self.name,self.ablood))

    def __str__(self):
        return '%s 还剩下 %s 血' % (self.name, self.blood)

xm = hero('西门吹雪',100,random.randint(10,20),random.randint(10,20))
ygc = hero('叶孤城',100,random.randint(10,20),random.randint(10,20))

x=[1,2]

while xm.blood>=0 or ygc.blood>=0:
    if xm.blood<=0:
        print('%s获胜'%ygc.name)
        break
        pass
    elif ygc.blood<=0:
        print('%s获胜'%xm.name)
        break
    if 10<=xm.blood <=20:
        xm.addblood()
        pass
    elif 10 <= ygc.blood <= 20:
        ygc.addblood()
        pass
    if random.choice(x)%2==0:
        xm.tong(ygc)
        print(ygc)
        print(xm)
    else:
        ygc.tong(xm)
        print(ygc)
        print(xm)
    print('***'*10)
    time.sleep(1)
    pass
```

> 本人博客：[https://blog.csdn.net/weixin_46654114](https://blog.csdn.net/weixin_46654114)
> 本人b站求关注：[https://space.bilibili.com/391105864](https://space.bilibili.com/391105864)
> 转载说明：跟我说明，务必注明来源，附带本人博客连接。

请给我点个赞鼓励我吧
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507113619405.png#pic_center)