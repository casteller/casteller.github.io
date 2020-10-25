---
title: Jenkins拉取github仓库代码执行构建并自动发邮件通知
author: MZ-ZONE
top: true
cover: true
toc: true
mathjax: false
date: 2020-08-23 13:49:47
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/052.jpg
coverImg:
password:
summary:
tags: Jenkins
categories: Jenkins
---
Jenkins 常用的就是项目构建，一般构建都需要从版本控制平台上面拉取项目代码到 Jenkins 服务器上构建。我主要使用的版本控制平台是 GitHub，所以这里就分享一下 Jenkins + GitHub 的基本构建配置过程。
## 一、安装GitHub插件
进入Jenkins插件管理，搜索GitHub plugin插件进行安装
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(12).png)
## 二、新建项目
新建一个自由风格的项目，勾选github项目，填写项目的URL
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(3).png)
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(11).png)
### 源码管理

其实我们在安装github的时候需要配置公钥（git如何安装和使用自行百度），那么我们拉取远程库代码就需要配置私钥

Git的私钥文件

一般安装Git的时候，生成的公钥和秘钥都默认在下面这个目录下

![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(19).png)
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(6).png)
源码管理我们勾选Git，并点击【添加】
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(14).png)
弹出框中按照标记内容进行添加
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(1).png)
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(7).png)
### 构建环境

我们这里选择每次构建之前清空一下Jenkins工作空间，避免拉取的代码有冲突
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(8).png)
选择执行windows批处理命令
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(5).png)
### 构建后操作
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(16).png)
修改下面的配置如图：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(13).png)
default content 是
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(10).png)
接下来我们手动构建一次看看是否能成功
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(15).png)
可以看到Jenkins工作空间已经拉取到了GitHub上面的项目代码
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(17).png)
自动打开了浏览器并运行自动化代码
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(18).png)
运行成功之后自动发了邮件，并且自动将测试报告发送到了邮件附件里
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(2).png)
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(4).png)
来看一下我们的报告
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/082301%20(9).png)
本次教程参考了https://www.cnblogs.com/linuxchao/  感谢大佬