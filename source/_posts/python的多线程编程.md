---
title: python的多线程编程
tags:
  - python
abbrlink: 39342
date: 2020-10-31 20:51:38
---



前言：

> 这是我看了这位[b站老师](https://www.bilibili.com/video/BV1fz4y1D7tU?p=16)做的笔记，听课完后觉得很简单，感觉我这笔记还写得有点啰嗦，**线程和进程**原理差不多，看了进程就可以跳着看线程了（反正我是这样的，哈哈）


## 一. 多任务介绍
1. **多任务**：同一时间打开多个任务。比如一台计算机上同时打开百度，和谷歌
2. **并发** ：在一段时间内 **交替** 去执行多个任务。比如对于单核cpu处理多任务，操作系统轮流让各个**任务交替执行**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201030200207254.png#pic_center)
 3. **并行**： 在一段时间内**真正的同时一起** 执行多个任务。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201030200452483.png#pic_center)

## 二. 进程
####  2.1 进程的介绍

> python中可以使用**多进程** 来实现**多任务**。

1. **进程的概念**：是资源的最小单位，，它是**操作系统**进行**资源分配**和**调度运行**的基本单位。通俗理解：一个正在运行的程序就是一个进程。例如qq等，都是一个进程
2. 多进程作用
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201030201224195.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjY1NDExNA==,size_16,color_FFFFFF,t_70#pic_center)
3. 进程在python中的创建步骤:

```python
#1. 导包
import multiprocessing
#2. 通过进程类创建进程对象
进程对象=multiprocessing.Process(target=任务名)
#3. 启动进程执行任务
进程对象.start()
```

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20201030201714242.png#pic_center)
练习：

```python
import multiprocessing
import  time

#创建两个任务

def sing():
    for i in range(3):
        print('唱歌...')
        time.sleep(1.5)
def dance():
    for i in range(3):
        print('跳舞..')
        time.sleep(1.5)

if __name__=='__main__':#main是主进程
    #使用进程类创0建进程对象
    #target指定执行函数名.记住：一定要指定
    sing_process=multiprocessing.Process(target=sing)
    dance_process=multiprocessing.Process(target=dance)
    #使用进程对象启动进程执行指定任务
    sing_process.start()
    dance_process.start()
'''输出
唱歌...
跳舞..
唱歌...
跳舞..
唱歌...
跳舞..

'''
```

#### 2.2 进程执行带有参数的任务
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201031175043874.png#pic_center)

**练习**：将上面代码3改为num
```python
import multiprocessing
import  time
#创建两个任务
def sing(num):
    for i in range(num):
        print('唱歌...')
        time.sleep(1.5)
def dance():
    for i in range(num):
        print('跳舞..')
        time.sleep(1.5)
if __name__=='__main__':
    sing_process=multiprocessing.Process(target=sing,args=(3,))#按照参数顺序
    dance_process=multiprocessing.Process(target=dance,kwargs={"num":2})#保证参数名一致就行
    #使用进程对象启动进程执行指定任务
    sing_process.start()
    dance_process.start()
    '''
    跟上述代码输出一样
	'''
```
#### 2.3 获取进程编号

> 作用：当程序进程多时，没办法区分主进程和子进程，为了方便管理给每个进程设定编号

注意：需要导入os包
获取当前进程编号：`os.getpid`
获取父进程编号：`os.getppid`

```python
import multiprocessing
import  time
import os#导入os
#创建两个任务

def sing():
        print('唱歌...')
        print("当前唱歌进程编号",os.getpid())
        print("获取父进程编号",os.getppid())
        time.sleep(1.5)

if __name__=='__main__':
    #使用进程类创0建进程对象
    #target指定执行函数名.记住：一定要指定
    print("当前主机进程编号",os.getpid())
    sing_process=multiprocessing.Process(target=sing)
    #使用进程对象启动进程执行指定任务
    sing_process.start()
    '''输出
    当前主机进程编号 7744
	唱歌...
	当前唱歌进程编号 20328
	获取父进程编号 7744
	'''
```

#### 2.4  守护进程
听到守护，是不是想到你那个夜晚对呀发誓要守护她一生一世

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020103120480518.gif#pic_center)
这里的守护可不一样

让我们来看看**守护进程**是什么：
<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

1. 一般情况下，主进程会等待子进程执行完后在结束，那么如何设置**主进程结束子进程也结束**，不再执行代码呢？
2. 设置守护主进程方式：`子进程对象.daemon=True`
3. 不多说，上代码

```python
import multiprocessing
import time

def work():
    for i in  range(10):
        print("工作中。。。")
        time.sleep(0.2)
if __name__=='__main__':
    #创建子进程
    sum_process=multiprocessing.Process(target=work)
    sum_process.daemon=True#设置守护主进程，主进程退出后子进程直接销毁，不在执行
    sum_process.start()
    time.sleep(1)
    print("主进程执行完成")
    '''输出
    工作中。。。
	工作中。。。
	工作中。。。
	工作中。。。
	工作中。。。
	主进程执行完成
    '''
```

> 你们可以去掉守护进程自己去试一下，后面还会运行子进程

## 三. 线程
#### 3.1 线程介绍

> 在python中还可以使用**多线程**完成**多任务**


**为什么使用**

1. 进程是分配资源的最小单位, 一旦创建一个进程就会分配一定的资源,就像跟两个人聊QQ就需要打开两个QQ软件-样是比较浪费资源的.
2. 线程是**程序执行的最小单位**,实际上进程只负责分配资源,而利用这些资源执行程序的是线程,也就说进程是线程的容器,**一个进程中最少有一个线程**来负责执行程序.同时线程自己不拥有系统资源，只需要一点儿在运行中必不可少的资源，但它可与同属一一个进程的其它线程**共享进程所拥有的全部资源**。这就像通过一个QQ软件(一个进程)打开两个窗口(两个线程)跟两个人聊天一样,实现多任务的同时也节省了资源.

**总结：**

> （1）线程是程序执行的最小单位. 
> （2）同属一个进程的多个线程**共享进程所拥有的全部资源.**

#### 3.2 创建步骤


1. 导入线程模块

```python
import threading
```
2. 通过线程类创建线程对象

```python
线程对象=threading.Thread(target=任务名)
```
3. 启动线程执行任务

```python
线程对象.start()
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201031194509748.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjY1NDExNA==,size_16,color_FFFFFF,t_70#pic_center)

**代码实例**
```python
import threading
import  time

#创建两个任务

def sing():
    for i in range(3):
        print('唱歌...')
        time.sleep(1.5)
def dance():
    for i in range(3):
        print('跳舞..')
        time.sleep(1.5)

if __name__=='__main__':
    #使用进程类创0建进程对象
    #target指定执行函数名.记住：一定要指定
    sing_process=threading.Thread(target=sing)
    dance_process=threading.Thread(target=dance)
    #使用进程对象启动进程执行指定任务
    sing_process.start()
    dance_process.start()
```
**代码解析：跟进程不同，唱歌跳舞是同时出现的，遍历了三次**



#### 3.3 守护线程
1. 主线程会等待所有的子线程执行结束再结束，除非设置子线程守护主线程
2. 设置守护主线程有两种方式:

（1）`threading.Thread(target=work, daemon=True)`

（2）`线程对象.setDaemon(True)`


差不多跟进程一样，就不上代码了

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201031202053293.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjY1NDExNA==,size_16,color_FFFFFF,t_70#pic_center)



#### 3.4 多进程执行顺序
介绍：多进程执行时无序的，是由**cpu调度决定某个线程先执行的**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201031201115320.gif#pic_center)
**上代码**
```python
import threading
import time

def task():
    time.sleep(2)
    #current_thread():获取当前线程的线程对象
    thread=threading.current_thread()
    print(thread)
if __name__== '__main__':
    for i in range(5):
        sub_thread=threading.Thread(target=task)
        sub_thread.start()
 '''输出
 <Thread(Thread-2, started 12040)>
<Thread(Thread-3, started 3856)>
<Thread(Thread-1, started 20524)>
<Thread(Thread-4, started 7800)>
<Thread(Thread-5, started 20360)>
 '''
```
我们可以看到，输出的是23145，顺序是被打乱的，所以多进程是无序的


## 四. 进程和线程对比

1.关系对比
（1）**线程**是依附于**进程**的，没有进程就没线程
（2）一个进程默认提供**一条线程**，进程可以创建**多个线程**
2. 区别对比
（1）创建**进程**开销比**线程**大
（2）**进程**是**操作系统资源分配**的基本单位，**线程**是**cpu调度**的基本单位
（3）**线程**需要依附**进程**才可以运行
3. 优缺点对比

（1）**线程**可以用**多核**，进程不能
（2）开销的大小


> 本人博客：[https://blog.csdn.net/weixin_46654114](https://blog.csdn.net/weixin_46654114)
> 本人b站求关注：[https://space.bilibili.com/391105864](https://space.bilibili.com/391105864)
> 转载说明：跟我说明，务必注明来源，附带本人博客连接。

请给我点个赞鼓励我吧
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507113619405.png#pic_center)