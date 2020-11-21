---
title: 第五天——python内置函数
tags:
  - python
categories:
  - python基础
abbrlink: 22027
date: 2020-10-31 14:21:03
---





前言

> 这是我听老师讲课做的笔记,考试要看的。 
>
> 作者：RodmaChen 
>
> 关注我的[csdn博客](https://blog.csdn.net/weixin_46654114)，更多数据结构与算法知识还在更新

##  一. 内置函数介绍

> 所谓内置函数就是python安装后就自带有的函数

![image-20201031142425428](E:\图片\博客图片\image-20201031142425428.png)



## 二. 数学运算练习

> abs()	round()	pow()	divmod()	max()	min()	sum()	eval()

```python
# 求绝对值
print(abs(-10))

#近似取值
print(round(2.5))

#求指数
print(pow(2,3))# 输出2的3次幂
print(pow(2,3,3))# 输出2的3次幂除于3的余数
# 求商和余数
print(divmod(7,3))

# 求最大最小值
a=(100,10,25,34)
print(max(a))
print(min(a))

# 求和

print(sum( (10,100 )))# 输出的是元组类型的整数
print(sum([10,100],2))# 也可以输出列表的,并且可以在外面添加参数，默认为0

# 执行字符表达式
a=1
b=2
print(eval('a+b'))
print(eval('a+b+c',{'a':1,'b':2,'c':3}))

'''输出
10
2
8
2
(2, 1)
100
10
110
112
3
6
'''
```



## 三.类型转换

> int()	float()	str()	ord()	chr()	bool()	bin()	hex()	oct()	list()	tuple()	dict()	bytes()

```python
# 整型
print(int(3.3))
# 浮点数
print(float(3))

# 字符转数字
print(ord('A'))
# 字符类型
a=1
print(type(a))
print(type(str(a)))

# 布尔型
a={}
print(bool(a))

# 进制转换
print(bin(17))
print(hex(17))
print(oct(17))

# 转换
a=()
print(type(a))# 查看a的类型为元组
print(type(list(a)))# 转为list了

#创建字典
print(dict(a='chen',b=30,c='python'))
dictA={'a':'chen','b':30,'c':'python'}# 不能直接定义函数写入print语句中
print(dictA)

# 转为字节数组
print(bytes('中'.encode('utf-8')))
print(bytes('中'.encode('gbk')))
print(bytes('zhon'.encode('gbk')))
print(bytes('zhon'.encode('utf-8')))

'''输出
3
3.0
65
<class 'int'>
<class 'str'>
False
0b10001
0x11
0o21
<class 'tuple'>
<class 'list'>
{'a': 'chen', 'b': 30, 'c': 'python'}
{'a': 'chen', 'b': 30, 'c': 'python'}
b'\xe4\xb8\xad'
b'\xd6\xd0'
b'zhon'
b'zhon'

'''
```



## 四. 序列操作

> all()	any()	sorted()	reverse()	range()	zip()	enumerate()

```python
# 判定参数
li=[1,2,3,0]
print(all(li))
print(any(li))#只要不全是false的元素就返回true

# 排序

print(sorted([2,4,7,1,8]))#排序默认为reverse=false升序排序
print(sorted([2,4,7,3,9],reverse=True))# True的时候是降序排序
print(sorted(['a','b','C','D','d'],key=str.lower))  # 字符串无关大小写排序


# 反向列表
a=[1,2,3,4]
print(a.reverse())# 无返回值会输出None
print(a)# 在输出a时会发现倒序了

# 创建一个整数列表
for item in range(1,5):#range 左闭又开所以输出1~4的数
    print(item,end=" ")
    pass
print('\n')
# zip()

print(zip([1,2,3],['a','b','c']))
a=zip([1,2,3],['a','b','c'])
print(list(a))
print(list(zip([1,2,3],['a','b'])))
print('\n')
#enumerate()索引

seasons =  ['spring','summer','fall','winter']
print(list(enumerate(seasons)))
print(list(enumerate(seasons, start=5)))#从第五个主键开始索引

'''输出
False
True
[1, 2, 4, 7, 8]
[9, 7, 4, 3, 2]
['a', 'b', 'C', 'D', 'd']
None
[4, 3, 2, 1]
1 2 3 4 

<zip object at 0x0000021E23583280>
[(1, 'a'), (2, 'b'), (3, 'c')]
[(1, 'a'), (2, 'b')]


[(0, 'spring'), (1, 'summer'), (2, 'fall'), (3, 'winter')]
[(5, 'spring'), (6, 'summer'), (7, 'fall'), (8, 'winter')]
'''
```



## 五. set 集合

> set（集合） 也是python中的一种数据类型，是一个无序且不重复的元素集合
>
> 操作函数：add()	clear()	difference()	intersection()	union()	pop()	discard()	update()

创建集合方式?

第一种方式：

```python
set1 = {"1","2"}
```

第二种方式

```python
list1 = ['1','5','4','3']

set2 = set(list1)
```

**练习**：

```python
setA={'1','2'}
# 添加
setA.add('3')# 不能直接放入函数中，没有返回值
print(setA)

# 清空
setA.clear()
print(setA)

# 差交并

a = {32,12,34}
b = {12,43,23}
print(a.difference(b))#差a-b
print(a.intersection(b))#交a&b
print(a.union(b))#并a|b

#参数的移除和获取
a={12,13,14,15}
print(a.pop())
print(a)
a.discard(13)#移除指定元素
print(a)

#更新
a={1,2,3}
b={4,5,6}
a.update(b)
print(a)
'''输出
{'3', '1', '2'}
set()
{32, 34}
{12}
{32, 34, 23, 43, 12}
12
{13, 14, 15}
{14, 15}
{1, 2, 3, 4, 5, 6}
'''
```

## 六. 练习

指定一个列表，列表里含有唯一一个只出现过一次的数字。写程序找出这个“独一无二”的数字

```python
li=[1,3,4,3,3,5,7,2,4,2,5,2,1]
set1=set(li)
print(set1)
for i in set1:
    li.remove(i)#remove() 函数用于移除列表中某个值的第一个匹配项。
    pass
print(li)
set2=set(li) #set2中为原来li中有重复的数字集合
print(set2)
for i in set1: #set1中数据全部去重后形成的集合
    if i not in set2:
        print(i)
        pass
    pass
'''输出
{1, 2, 3, 4, 5, 7}
[3, 3, 4, 2, 5, 2, 1]
{1, 2, 3, 4, 5}
7
'''
```



> 本人博客：[https://blog.csdn.net/weixin_46654114](https://blog.csdn.net/weixin_46654114)
> 本人b站求关注：[https://space.bilibili.com/391105864](https://space.bilibili.com/391105864)
> 转载说明：跟我说明，务必注明来源，附带本人博客连接。

请给我点个赞鼓励我吧
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507113619405.png#pic_center)