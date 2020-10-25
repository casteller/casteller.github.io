---
title: python连接数据库批量插入数据
author: MZ-ZONE
top: false
cover: true
toc: true
mathjax: false
date: 2020-08-23 15:20:49
img:
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/038.jpg
coverImg:
password:
summary:
tags: 
   - [Mysql]
   - [python]
categories: 
   - [python]
   - [数据库]
---

``` python
思路：连接数据库-获取游标-拼好sql-执行sql-提交数据-关闭游标-关闭链接
import MySQLdb,time,pprint
import random
t = int(time.time())
#链接数据库
connection = MySQLdb.connect(host="127.0.0.1",
                     user="songqin",
                     passwd='songqin',
                     db='plesson',
                     charset = "utf8")
#获取游标
c = connection.cursor()
sql = "select * from sq_course"
for i in range(1,11):
    names = random.choice(['语文','数学','外语','物理','化学'])+str(i)
    descs = "课程描述"+str(i)
    idx = str(i)
    sql1 = "INSERT INTO sq_course (name,`desc`,display_idx) VALUES('%s','%s','%s');" %(names,descs,idx)
    #执行SQL
    raw = c.execute(sql1)
    #插入数据完后提交数据
    connection.commit()
 
raw1 = c.execute(sql)
pprint.pprint(c.fetchall())
#关闭游标
c.close()
#连接关闭
connection.close()
```
