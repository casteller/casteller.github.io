---
title: Django安装教程
author: MZ-ZONE
top: false
cover: true
toc: true
mathjax: false
date: 2020-08-23 18:31:47
img:
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/035.jpg
coverImg:
password:
summary:
tags: 'Django'
categories: 'Django'
---
在安装 Django 前，系统需要已经安装了Python的开发环境。接下来我们来具体看下不同系统下Django的安装。
## Window 下安装 Django
如果你还未安装Python环境需要先下载Python安装包。
1、Python 下载地址：https://www.python.org/downloads/
2、Django 下载地址：https://www.djangoproject.com/download/
注意：目前Django 1.6.x以上版本已经完全兼容Python 3.x。
### Python 安装(已安装的可跳过)
安装Python你只需要下载python-x.x.x.msi文件，然后一直点击"Next"按钮即可。
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/install1.png)
安装完成后你需要设置Python环境变量。 右击计算机->属性->高级->环境变量->修改系统变量path，添加Python安装地址，本文实例使用的是C:\Python33，你需要根据你实际情况来安装。
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/install2.png)
### Django 安装
下载 Django 压缩包，解压并和Python安装目录放在同一个根目录，进入 Django 目录，执行python setup.py install，然后开始安装，Django将要被安装到Python的Lib下site-packages。
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/install3.jpeg)
然后是配置环境变量，将这几个目录添加到系统环境变量中： C:\Python33\Lib\site-packages\django;C:\Python33\Scripts。 添加完成后就可以使用Django的django-admin.py命令新建工程了。
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/install4.jpeg)
### 检查是否安装成功
输入以下命令进行检查:

```
>>> import django
>>> django.get_version()
```
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/install5.jpeg)
如果输出了Django的版本号说明安装正确。
