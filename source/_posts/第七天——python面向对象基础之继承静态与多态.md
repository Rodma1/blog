---
title: 第七天——python面向对象基础之继承静态与多态
tags:
  - python
categories:
  - python基础
abbrlink: 34188
date: 2020-10-31 15:26:44
---



前言

> 这是我听老师讲课做的笔记,考试要看的。 
>
> 作者：RodmaChen 
>
> 关注我的[csdn博客](https://blog.csdn.net/weixin_46654114)，更多数据结构与算法知识还在更新

## 一. 析构方法



介绍：当一个对象被删除或者被销毁时，python解释器也会默认调用一个方法，这个方法为__del__()方法，也称为析构方法



```python
# 

class Animal(object):
    def __init__(self,name):#定义__init__方法
        self.name=name#实例属性
        print('init方法被调用')
    def __del__(self):
        print('程序执行结束，自动调用del方法销毁对象%s'%self.name)
dog=Animal('狗')
# 或者直接删除对象也可以自动调用del方法
del dog

input('程序等待中')#这是一个输入函数，说明程序还没结束，可是del方法被执行了

'''输出
init方法被调用
程序执行结束，自动调用del方法销毁对象狗
程序等待中
'''
```

总结：

> 1、当整个程序脚本执行完毕后会自动调用__del__方法
>
> 2、当对像被手动销毁时也会自动调用 __del__ 方法
>
> 3、析构函数一般用于资源回收，利用__del__方法销毁对象回收内存等资源



## 二. 继承,调用与重写

#### 2.1 单继承

```python
# 在现实生活中，继承一般指的是子继承父辈的财产。在面向对象中继承也是同样道理，不过子继承了父的所有类

#比如：猫和狗都是动物（动物有吃，喝的方法），他们有相同属性，我们一个个定义太麻烦

class Father(object):# 父类
    print('全部财产')
    def interest(self):
        print('都是儿子的')
    pass
class Sun(Father):# 子类
    pass

Sun();#子类继承了父类
a=Sun();
a.interest();#子类继承了父类的方法
'''输出
全部财产
都是儿子的
'''
```

#### 2.2 多继承

```python
#子类可以继承一个父类，那是否可以继承两个父类或多个呢？答案是肯定的，这就是python的多继承
# 一对多，多对一的关系

class Father1(object):
    def a(self):
        print('第一个父亲')
        pass
    def Repeat(self):
        print('这是第一个父亲的同名方法')
class Father2(object):
    def b(self):
        print('第二个父亲')
        pass
    def Repeat(self):
        print('这是第二个父亲的同名方法')
class sun(Father1,Father2):#一个儿子继承两个父亲
    pass
c=sun();#创建对象
c.a();# 调用父类方法
c.b();

# 如果同名调用哪个

c.Repeat();#输出结果是调用了第一个父亲的

# 我们可以通过__mro__函数查看解析顺序
print(sun.__mro__)
#(<class '__main__.sun'>, <class '__main__.Father1'>, <class '__main__.Father2'>, <class 'object'>)
'''输出
第一个父亲
第二个父亲
这是第一个父亲的同名方法
(<class '__main__.sun'>, <class '__main__.Father1'>, <class '__main__.Father2'>, <class 'object'>)
'''
```



#### 2.3 继承传递和重写父类



```python
# 继承传递就是爷爷给爸爸，爸爸给儿子

class GrandFather(object):
    def eat(self):
        print('吃饭')
        # 继承  GrandFather 类
class Father(GrandFather):
    def fight(self):
        print('爸爸是用脚打儿子')
    pass# 继承 Father类
class Son(Father):
    def fight(self):
        print('儿子不给爸爸打')
    pass
lg = Son()
lg.eat()#调用了爷爷吃的方法

# 重写父类方法
ll=Father();#创建父类对象
ll.fight();
lg.fight();#从写了父类figh方法
'''输出
吃饭
爸爸是用脚打儿子
儿子不给爸爸打
'''
```



#### 2.4 调用父类方法

```python
#如果在子类中有一个方法需要父类的功能，并且又要添加新的功能。如果直接重写父类方法，那么就要重复写很多代码。那么这就要调用父类方法
class Father(object):
    def __init__(self,name):
        self.name=name
        pass
class sun(Father):
    def __init__(self,name):#重新构建父类方法
        #第一种
        super(sun, self).__init__(name)
        # 第二种方法
        #super().__init__(name)
        # 第三种方法
        #Father.__init__(self,name)
        # 添加新的功能
        self.name+='你好'
        print(self.name)
a=sun('dog')
```



## 三. 多态



```python
# 所谓多态：定义时的类型和运行时的类型不一样，此时就成为多态。后面统一调用
# 案例演示
class Animal:
    '''
    父类【基类】
    '''
    def say_who(self):
        print('我是一个动物....')
        pass
    pass
class Duck(Animal):
    '''
      鸭子类 【子类】 派生类
    '''
    def say_who(self):
        '''
        在这里重写父类的方法
        :return:
        '''
        print('我是一只漂亮的鸭子')
        pass
    pass
class People:
    def say_who(self):
        print('我是人类')
    pass

class student(People):
    def say_who(self):
        print('我是一年级的学习 张明')
    pass
#定义一个调用方法
def commonInvoke(obj):
    '''
        统一调用的方法
        :param obj: 对象的实例
        :return:
        '''
    obj.say_who()
    pass
listA=[Duck(),student()]#定义一个列表存放子类
for item in listA:#遍历列表,循环调用函数，输出say_who()
    commonInvoke(item)
'''输出
我是一只漂亮的鸭子
我是一年级的学习 张明
'''
```



## 四. 类属性和实例属性



```python
# 属性：类属性和实例属性
# 类属性 就是类对象所拥有的属性
# 类属性是可以 被类对象和实例对象共同访问使用的
# 实例属性只能由实例对象所访问

class Test(object):
    Ch='python'#类属性
    def __init__(self,name):
        self.name=name#实例属性
        pass
test=Test('love')#创建实例对象
print(test.Ch)#可以访问类属性
print(Test.Ch)#可以访问
#print(Test.name)#类对象不可以访问实例属性
print(test.name)#实例对象可以访问实例属性
#test.Ch='刘德华'  #通过实例对象 对类属性进行修改 可以吗? 不可以的，
#print(Test.Ch)类属性没有更改

#可是通过类对象对实例对象进行修改就可以，这相当于一个等级，先类才能到方法

'''输出
python
python
love
'''
```





## 五. 类方法和静态方法

1. **类方法**：类对象所拥有的方法，需要用装饰器@classmethod来标识其为类方法，对于类方法，第一个参数必须是类对象，一般以cls作为第一个参数，类方法可以通过类对象，实例对象调用
2. **对比**：

> （1）**类方法**的第一个参数是类对象`cls`，通过cls引用的类对象的属性和方法
>
> （2）**实例方法**的第一个参数是实例对象`self`，通过self引用的可能是类属性、也有可能是实例属性(这个需要具体分析)，不过在存在相同名称的类属性和实例属性的情况下，实例属性优先级更高。
>
> （3）**静态方法**中**不需要额外定义参数**，因此在静态方法中引用类属性的话，必须通过类对象来引用。





```python
class  People:
    country='china'
    #类方法 用 classmethod 来进行修饰
    @classmethod
    def get_country(cls):
        return cls.country #访问类属性
        pass
    @classmethod
    def change_country(cls,data):
        cls.country=data #修改类属性的值  在类方法中
        pass
    @staticmethod
    def getData():
        return People.country  #通过类对象去引用
        pass
    @staticmethod
    def add(x,y):
        return x+y
        pass


print(People.add(10,56)) #带有参数的静态方法

# print(People.getData())

# print(People.get_country()) #通过类对象去引用
p=People()
print(p.getData()) #注意 一般情况下 我们不会通过实例对象去访问静态方法
# print('实例对象访问 %s'%p.get_country())
# print('-----------------修改之后---------------------------')
# People.change_country('英国')
# print(People.get_country()) #通过类对象去引用

# 为什么要使用静态方法呢
# 由于静态方法主要来存放逻辑性的代码，本身和类以及实例对象没有交互，
# 也就是说，在静态方法中，不会涉及到类中方法和属性的操作
# 数据资源能够得到有效的充分利用

# demo  返回当前的系统时间
import  time # 引入第三方的时间模块
class TimeTest:
    def __init__(self,hour,min,second):
        self.hour=hour
        self.min = min
        self.second = second

    @staticmethod
    def showTime():
        return time.strftime("%H:%M:%S",time.localtime())
        pass
    pass

print(TimeTest.showTime())
t=TimeTest(2,10,15)
print(t.showTime()) #没有必要通过这种方式去访问 静态方法
```





