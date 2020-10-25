---
title: Jmeter连接数据库
author: MZ-ZONE
top: false
cover: true
toc: true
mathjax: false
date: 2020-08-23 15:11:03
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/042.jpg
coverImg:
password:
summary:
tags: Mysql
categories: 
   - [Jmeter]
   - [数据库]
---
jmeter要链接mysql数据库，首先得下载mysql jdbc驱动包（注：驱动包的版本一定要与你数据库的版本匹配，驱动版本低于mysql版本有可能会导致连接失败报错）我这里下载的是mysql-connector-java-5.1.23-bin.jar,。

下载地址：http://www.java2s.com/Code/Jar/m/Downloadmysqlconnectorjava5123binjar.htm

下载好之后解压将jar包放到\jmeter\apache-jmeter-5.0\lib目录下

好，接下来进入正题！

## 1、添加一个线程组
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_03%20(2).png)
## 2、线程组下新建一个JDBC Connection Configuration配置元件，详细配置如下图：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_03%20(3).png)
## 3、然后添加一个取样器 JDBC request
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_03%20(4).png)
## 4、最后添加一个监听器 查看结果树查看响应结果
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_03%20(1).png)
好了，以上就是一个最简单的jmeter连接数据库的脚本