---
title: Charles的安装与使用说明
author: MZ-ZONE
top: false
cover: true
toc: true
mathjax: false
date: 2020-09-07 16:21:00
img: 
coverImg: 
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/012.jpg
password:
summary:
tags: 
    - [charles]
categories:
    - [charles]
---
## 一、安装
在网上找到的破解安装步骤，直接抄过来
 http://charles.iiilab.com/    #破解注册
下载Charles Proxy 4.1.2版本，百度云盘下载 或 去官网下载
安装后先打开Charles一次（Windows版可以忽略此步骤）
在这个网站(http://charles.iiilab.com/)下载破解文件 charles.jar
替换掉原文件夹里的charles.jar 
Mac: /Applications/Charles.app/Contents/Java/charles.jar
Windows: C:\Program Files\Charles\lib\charles.jar
      恭喜！破解注册成功！
## 二、使用前基本设置
### 1.手机设置代理
注意点：Charles默认端口就是8888，手机连接的wifi必须和电脑连接的wifi是同一个局域网。

charles设置代理端口号8888：Proxy→ Proxy Settings
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/62-139168698.png)
手机设置代理，连接wifi，点开设置http代理，选择手动，服务器填写charles所在本机的ip地址，端口号8888
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/5-1359099946.png)
### 2.SSL代理设置，允许抓取https协议
Proxy→SSL Proxying Settings→勾取Enable SSL Proxying→add→添加想要抓取的域名和端口号，以抓取阿波罗app数据为例
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/21-550942315.png)
## 三、拦截某个软件的接口数据
手机代理到电脑，charles会出现弹窗，询问allow还是deny，选择allow，连接成功。
通常情况下，我们需要对网络请求进行过滤，只监控向指定目录服务器上发送的请求。
在Charles的菜单栏选择"Proxy"->"Recording Settings"，然后选择Include栏，选择添加一个项目，然后填入需要监控的协议，主机地址，端口号。这样就可以只截取目标网站的封包了。如下图截取阿波罗app数据：
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/7-1981590493.png)
如果只测试一个功能的情况下，可以只截取单个接口，例如测试阿波罗首页广告，只需截取splash接口，添加并勾选。
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/27-590574806.png)
勾选Proxy →Start Recording，开启抓取记录，可以在charles界面看到你所过滤的网络请求，以阿波罗app为例：
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/65-334654904.png)
Charles主要提供2种查看封包的视图，分别名为“Structure”和"Sequence"。
Structure视图将网络请求按访问的域名分类。
Sequence视图将网络请求按访问的时间排序。
大家可以根据具体的需要在这两种视图之前来回切换。
对于某一个具体的网络请求，你可以查看其详细的请求内容和响应内容。如果响应内容是JSON格式的，那么Charles可以自动帮你将JSON内容格式化，方便你查看。
## 四、更改返回数据来测试各种情况
### 1.强大的mapping功能
#### a.Map Local
可以将远程的某个文件代理到本地文件，进行调试。使用方法如下：
Tools→Map Local→勾选Enable Map Local→Add→填入需要映射本地文件的协议，主机地址，端口号
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/2-2135000769.png)
本地文件可以是自己造的测试数据，也可以是接口返回的数据保存到本地再进行修改，只需先将接口返回数据进行保存到本地：点击某接口response，右击save response。
#### b.Map Remote
Map Remote的功能原理和Map Local的原理相同，都是替换请求，只不过Map Local替换的请求为本地文件，而Map Remote替换的请求为线上请求。
使用方法：Tools→Map Remote→勾选Enable Map Remote→Add→填入需要替换请求的协议，主机地址，端口号。
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/9-1993174545.png)
如图，splash接口映射到entry接口，splash接口访问的是entry接口的数据。
### 2.断点功能
我们可以通过使用断点功能来篡改请求的数据或者返回的数据，达到模拟的效果，已测试阿波罗app为例方法如下：
类似于mapping，我们可以针对接口右键选择"BreakPoints",这样这个接口就被加入到断点状态了
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/87-611953958.png)
需要进一步修改断点的属性，可以在菜单栏"Proxy"–>"Breakpoints Settings"里进行添加删除或者修改，配置方式和mapping雷同，并且可以选择这个断点是在request还是response，还是两者都要。
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/2-2045830780.png)
这个时候再刷新app界面，会直接跳转到断点模版，这个时候你可以在对应状态情况下修改request或者response,然后点击下方按钮“Execute”。
跳转到断点界面，先点击下方执行按钮“Execute”。
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/80-293810778.png)
然后点开Edit Response界面，选择JSON格式，格式清晰，方便修改，直接在上面进行数据修改，改成你想要测试的数据，然后点击执行按钮
![image](http://qfgo6n0sy.hn-bkt.clouddn.com/1-1679133438.png)
再次刷新app界面，然后app返回的是新改的数据，根据返回数据测试客户端显示是否正确。
