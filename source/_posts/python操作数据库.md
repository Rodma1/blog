---
title: python操作数据库.md
tags:
- python
abbrlink: 57497
date: 2020-10-30 16:04:26
categories:
- python操作数据库
---

## 1. 概述

1. Python 标准数据库接口为 Python DB-API，Python DB-API为开发人员提供了数据库应用编程接口。 

2. PyMySQL 是在 Python3.x 版本中用于连接 MySQL 服务器的一个实现库，Python2中则使用mysqldb。

3. PyMySQL 遵循 Python 数据库 API v2.0 规范，并包含了 pure-Python MySQL 客户端库。



## 2. 安装PyMySQL

1. 在使用 PyMySQL 之前，我们需要确保 PyMySQL 已安装。
   PyMySQL 下载地址：https://github.com/PyMySQL/PyMySQL。

2. 如果还未安装，我们可以使用以下命令安装最新版的 PyMySQL：

   ```python
    pip install PyMySQL
   ```

   



![image-20201030171305441](C:\Users\陈运智\AppData\Roaming\Typora\typora-user-images\image-20201030171305441.png)



## 3. 连接数据库：Connection



1.  ** 前提要求**：连接数据库之前，请确保已经创建了python数据库，以及students表,确认包导入

2.  **连接数据库**：Connection

   **Connection 连接对象拥有的方法**

   > close 关闭连接：连接数据库跟打开文件一样，操作完成之后需要关闭，否则会占用连接。
   > commit()提交：pymysql 默认开启事物，所以每次更新数据库都要提交
   > rollback()回滚：事物回滚
   > cursor()返回Cursor对象：用于执行sql语句并获得结果

   ```python
   from pymysql import  *
   conn=connect(host='127.0.0.1',user='root' , password='cyz', database='mybd'
                ,port=3306,charset='utf8')
   # 导入pymysql模块 
   # 创建连接对象 Connection对象 
   # host:数据库主机地址 
   # user:数据库账号 
   # password：数据库密码 
   # database : 需要连接的数据库的名称 
   # port: mysql的端口号 
   # charset: 通信采用编码格式 
   try:
       print('sucess')
   except Exception as ex:
       print(ex)
   #这里加个异常判断，如果出错就抛出异常，没有错就输出sucess
   ```

3. 创建Connection 对象：用于建立与数据库的连接 
   (1)获取cursor对象

   ```python
   cur = conn.cursor() # cursor对象用于执行sql语句
   ```

   (2)cursor对象拥有的方法

   > close()关闭cursor对象
   > execute(operation [, parameters ]) 执行语句，返回受影响的行数，可以执行所有语句
   > fetchone()获取查询结果集的第一个行数据，返回一个元组
   > fetchall()执行查询时，获取结果集的所有行，一行构成一个元组，再将这些元组装入一个元组返回

   

   

   ```python
   try:
       cur=conn.cursor()#赋值给对象cur执行sql语句
       '''查找'''
       cur.execute('select * from student')#''里面输入sql语句就可以
       result=cur.fetchall()#获取结果及所有数据
       #cur.fetchone()  # 获取结果集的第一条数据
       print(result)#打印结果,输出的是stupele元组形式
       for item in  result:
           # 按照元组的方式循环遍历
           print('姓名：{0}地址{1}'.format(item[1],item[2]))
       #print('sucess')
       
       '''插入'''
       res = cur.execute('insert into student VALUES (2018060808,"智" , "海南" );')#注意这里要""双引号
       print(res)  # 查看受影响的行数
       conn.commit()  # 提交事物
       
   except Exception as ex:
       print(ex)
   ```

   



> 本人博客：[https://blog.csdn.net/weixin_46654114](https://blog.csdn.net/weixin_46654114)
> 本人b站求关注：[https://space.bilibili.com/391105864](https://space.bilibili.com/391105864)
> 转载说明：跟我说明，务必注明来源，附带本人博客连接。

请给我点个赞鼓励我吧
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507113619405.png#pic_center)