---
title: Python pip下载速度慢? Windows设置国内源，用阿里云国内镜像加速
date: 2020-08-21 22:01:26
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/056.jpg
tags: 
   - [python]
   - [pip]
categories: 
   - python
cover: true
---
pip 提供了对 Python 包的查找、下载、安装、卸载的功能，是非常方便的 Python 包管理工具。但是，令人苦恼的是 pip 在国内的下载速度非常慢，速度常常只有每秒几十 K，甚至才几 K，小点的包还好，还能等，更多的时候，则是完全要把人逼疯的节奏。

这里，咪博士就教大家，如何在 Windows 下，为 pip 设置国内源。设置完成之后，速度可以达到每秒好几 M，快到飞起来。这里我们选用阿里云的国内镜像。毕竟有大金主支持，稳定性有保障。
## 一、新建 pip 配置文件夹
先在 windows “文件资源管理器” 地址栏 输入 %APPDATA% 按回车，打开程序自定义设置文件夹

然后，创建名为 pip  的文件夹，用于存放 pip 配置文件

![](http://qfgo6n0sy.hn-bkt.clouddn.com/0.png)
## 二、新建 pip 配置文件
在刚才创建好的 pip 文件夹中，新建 名为 pip.ini 的配置文件
![](http://qfgo6n0sy.hn-bkt.clouddn.com/1.png)
## 三、设置 pip 国内源 (使用 阿里云 国内镜像)
在 pip.ini 文件中输入以下内容，然后保存

```
[global]

index-url=http://mirrors.aliyun.com/pypi/simple/

[install]

trusted-host=mirrors.aliyun.com
```
如果嫌麻烦，也可以直接下载咪博士准备好的配置文件 https://pan.baidu.com/s/1o8xEWRK
## 四、验证设置
按 windows 徽标+ R，输入 cmd，按回车，调出 windows 命令行窗口
![](http://qfgo6n0sy.hn-bkt.clouddn.com/2.png)
尝试用 pip 安装一个比较大一点的包，譬如 kivy.deps.gstreamer (约 120 M)

```
python -m pip install kivy.deps.gstreamer
```
注意到 pip 从阿里云 (aliyun) 下载，速度达到了每秒 7.5 M，快到飞起来
![](http://qfgo6n0sy.hn-bkt.clouddn.com/3.png)
妈妈再也不用担心 pip 下载速度慢啦。
