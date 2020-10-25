---
title: Jenkins安装教程
author: MZ-ZONE
top: false
cover: true
toc: true
mathjax: false
date: 2020-08-23 14:27:03
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/051.jpg
coverImg:
password:
summary:
tags: Jenkins
categories: Jenkins
---
Jenkins安装方法有很多，本文主要介绍通用安装方式（傻瓜式安装）
## 一、下载
进入https://jenkins.io/download/ ，按需下载。如用于生产，建议下载Long-term Support (LTS) 版本，这样能够获得相对长期的维护；如想体验最新的功能，可尝试 Weekly 版本。可以直接下载特定系统专属的版本，也可下载 Generic Java package (.war) 。本文下载的是 Generic Java package (.war) ，这样对所有系统都通用。
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(1).png)
## 二、安装
本文采用Tomcat安装方式，首先需要安装Tomcat（Tomcat安装方法请自行百度），将下载下来的Jenkins.war包放到Tomcat的webapps目录下，然后启动Tomcat即可
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(2).png)
启动后会在webapps目录下生成一个Jenkins文件夹，然后我们访问http://localhost:18080/jenkins，即可看到如下界面：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(3).png)
这里需要填写管理员密码，由图中提示可知，Jenkins设置了一个初始的管理员密码，该密码存储在 /Users/itmuch.com/.jenkins/secrets/initialAdminPassword 文件中——只需可找到该文件，将其内容复制到图示的输入框中即可。点击 【继续】 按钮，将会出现类似如下的界面：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(4).png)
这里我们安装推荐的插件即可
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(5).png)
插件安装有点慢，有些插件有可能安装失败，不要紧，点击继续，然后会进入到如下界面：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(6).png)
填入账户信息后，进入完成页面：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(7).png)
安装完成！
## 三、配置 Jenkins 构建工具
### 3.1 进入 jenkins 主界面
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(8).png)
### 3.2 进入全局工具配置页面
点击 "系统管理" -> "全局工具配置"
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(31).png)
进入后配置构建工具
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(12).png)
### 3.3 配置 Maven
如果机器上已经安装了 Maven，则在 Maven_HOME 输入框中提供具体的安装路径。否则，你可以选择需要的 maven 版本，让 Jenkins 为你自动下载 maven。
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(13).png)
### 3.4 配置 JDK
同理，如果机器上已经安装了 JDK，则在 JAVA_HOME 输入框中提供具体的安装路径。否则，你可以选择需要的 JDK 版本，让 Jenkins 为你自动下载 JDK。
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(14).png)
### 3.5 配置 Git
如果之前没有为 Jenkins 安装 Git、Subversion（SVN）或 CVS 插件，可以在 "系统管理" -> "管理插件" 中安装。
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(10).png)
## 四、构建作业
构建作业是 Jenkins 构建过程的核心。
### 4.1 点击创建一个新任务，进入创建项目类型选择页面
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(11).png)
如果发现没有 "构建一个maven项目" 这一项，则需要安装 Maven Integration 插件，如下：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(9).png)
### 4.2 进入构建作业的详细页面
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(15).png)
### 4.3 源码管理
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(18).png)
### 4.4 构建触发器
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(16).png)
其中有 5 个参数，分别表示：

**MINUTE**：Minutes within the hour（0-59）

**HOUR**：The hour of the day（0-23）

**DOM**：The day of the month（1-31）

**MONTH**：The month（1-12）

**DOW**：The day of the week（0-7）where 0 and 7 are sunday

常用配置：

0 * * * * 为每个小时执行一次

0 1 * * * 为没天的凌晨1点执行一次，这种配置的设置，适合执行一些冒烟的测试用例

第一个参数：min，0-59

第二个参数：hour：0-23

第三个参数：day：0-31

第四个参数：month：1-12

第五个参数：week：0-7（0 和 7 代表 Sunday）

Jenkins 中 "Poll SCM" 和 "Build periodically"的区别

**Poll SCM**：定时检查源码变更（根据SCM软件的版本号），如果有更新就checkout最新code下来，然后执行构建动作，配置如下：

*/5 * * * * （每5分钟检查一次源码变化）

**  Build periodically**：周期进行项目构建（它不care源码是否发生变化），配置如下：

0 2 * * * （每天2:00 必须build一次源码）
### 4.5 构建
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(17).png)
在 "Build" 中，默认的项目根目录的 Root POM，即 pom.xml。如果 pom.xml 不在根目录下，就填入子目录，例如：cloud/pom.xml。

如果源码管理中选择 "None"，此处点 "高级..." 可以自定义工作空间中的项目地址，如下：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(19).png)
保存上面的构建作业：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(21).png)
## 五、构建
构建作业之后，就可以执行构建过程了。
### 5.1 执行构建的方式
第一种：点击任务名称的右边的小三角，然后点击 "立即构建"
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(22).png)
第二种：按照 "构建触发器" 中设置的 "日程表"定时自动触发构建
### 5.2 构建结果
第一列是 "上次构建状态显示"，是一个圆形图标，一般分为四种：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(25).png)
蓝色：构建成功；
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(28).png)
黄色：不确定，可能构建成功，但包含错误；
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(29).png)
红色：构建失败；
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(30).png)
灰色：项目从未构建过，或者被禁用；
如上显示蓝色，表示构建成功。
注意：手动触发构建的时间与自动定时构建的时间互不影响。
### 5.3 查看控制台输出
可以查看构建成功的控制台输出：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(26).png)
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(32).png)
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(33).png)
控制台信息显示将构建的 jar 包从项目的 target 目录下归档到了 jenkins 指定的目录下了
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(35).png)
此目录显示按照不同的构建编号，构建成功的项目
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(36).png)
这与该工程的构建历史中的编号相对应
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(34).png)
如果构建失败，可以通过查看构建失败的控制台输出，来得到具体的出错信息，便于调试
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(23).png)
点击后查看错误信息，如下：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(24).png)
第二列是 "编译晴雨表"，如下：
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(27).png)
如果看到你项目变成阴云或者下雨，说明你的项目稳定性不好，需要去查找原因，解决问题。
### 5.4 部署
如果要部署构建好的 war 包，可以在 Post Steps 中填上 shell 命令，直接用脚本部署。
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/photos/blogpic/20200823_02%20(20).png)
另一种方式是创建另外一个构建项目，手动触发部署。
无论用哪种方式，都是为了确保编译、部署是通过持续集成服务器完成的，而不是某台开发机器。
