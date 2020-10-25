---
title: Linux基础
author: MZ-ZONE
top: false
cover: true
toc: true
mathjax: false
date: 2020-08-23 18:41:03
img:
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/034.jpg
coverImg:
password:
summary:
tags: 'Linux'
categories: 'Linux'
---
# linux简介
## 1、基础命令
### 1.1、系统命令
init 0  -- 关机
init 6  -- 重启，也可以用reboot命令

pwd     -- 查看当前用户所在的位置（某个路径下），当前的操作路径
clear   -- 清空当前屏幕的内容
cal     -- 查看当月日历
date    -- 查看当前系统时间
ifconfig-- 查看网络配置信息
ping    -- 检测网络连通性，如ping 192.168.1.1是检测虚拟机是否与路由器相通
service [servername] restart  -- 重启xx服务，如network、mysqld、firewall，start启动，stop停用

cd      -- 路径跳转，如cd /usr/local是将操作路径切换到/usr/local下（绝对路径跳转）
        -- cd local/是将操作路径跳转到当前路径的下级路径（local/）下
        -- cd ./bin是将操作路径跳转到悠闲匹配到的bin目录（从根目录开始找，相对路径跳转）
cd ..   -- 返回上一级目录
ls      -- 查看当前路径下的文件（不含隐藏文件）
ls  -a  -- 查看当前路径下的所有文件（含隐藏文件）
ll      -- 查看当前路径下的文件属性（权限、所有者等信息）
ll  -a  -- 类似于ls -a
### 1.2、常用快捷键
Tab键    -- 补齐键，可以补齐命令、目录名。多次敲击此键还可以匹配相关文件或目录名
ESC键    -- 在vi编辑器中从编辑模式回到命令模式
Ctrl+C  -- 取消当前输入或中断当前操作
Ctrl+R  -- 查询最近使用过的命令
### 1.3、用户操作
useradd -- 添加普通用户，useradd [username]
passwd  -- 为指定用户设置密码，password [username]
su      -- 切换用户。高权限切换到低权限的用户，无需验证密码，反之需要验证密码
### 1.4、文件/文件夹操作
mkdir   -- 创建文件夹
        -- mkdir abc是在当前路径下创建一个叫abc的文件夹
        -- mkdir aa\ bb 创建一个名为'aa bb'的文件夹（有空格）
        -- mkdir aa bb 创建名字分别为aa和bb的两个文件夹
rmdir   -- 删除空文件夹
rm      -- 删除文件（有提示是否要删除），无法删除目录
rm -r   -- 删除非空目录（与提示，输入y/n），删除文件
rm -rf  -- 强制删除指定文件或目录（无提示）
cp      -- 复制并粘贴
cp -r /a/b . -- 将/a路径下的文件b复制到当前路径下，cp -r /a/b  /c/d是将/a路径下的b文件复制到/c/d目录下
mv      -- 剪切（移动）文件或路径，类似于cp的用法
mv a b  -- 将a文件命名为b（更名）

touch   -- 创建文件（文件要带扩展名），如touch abc.txt
vi      -- 创建并打开一个文件，进入默认的命令模式
### 1.5、vi编辑器
三大模式：
- 命令模式：通过命令进行文件内容操作（操作的命令无法显示），
    - G     光标跳转到末行首
    - gg    光标跳转到首行首
    - dd    删除光标所在的行
    - u     撤销上一步操作
    - yy    复制光标所在的行
    - p     粘贴复制的内容
    - i     进入编辑模式
    - :     进入末行模式
    - 
- 编辑模式：对内容进行编辑，可以通过ESC键返回命令模式

- 末行模式：执行文件的保存和退出等操作，可以通过ESC键返回命令模式
    - w     保存当前编辑的内容（write）
    - q     在没有修改文件内容的情况下退出（关闭文件）（quit）
    - wq    保存后退出（write before quit）
    - q!    强制退出（不保存退出）
    - set number    显示文件内容的行号
    
### 1.6、文件查看
cat      —— 一次性查看文件的内容（从头到尾）
tac      —— 反过来一次性显示文件内容（末行开始到首行）
more     —— 分页（按百分比）查看文件内容，查看时q键退出，vi进入编辑器，空格键翻页
less     —— 与more类似（没有百分比显示）,可以在查看过程中输入vi启用vi编辑器

tail a  -- 查看文件a最新的10行内容
tail -f -- 持续输出文件的最新内容（如linux有一些.out格式日志文件的内容是可以持续更新的）
tail -100f  -- 输出文件的最新100行内容，并持续输出后续更新的内容
### 1.7、文件压缩与解压
tar     -- 文件（或文件夹）压缩与解压，通过压缩参数或解压参数实现
tar -xvf -- 将压缩文件解压（tar/rar/war/zip）
tar -zvcf -- 对指定文件（或文件夹）进行压缩，如tar -zvcf a.tar a是将a文件（或文件夹）压缩为a.tar
### 1.8、件的安装和卸载
手动安装：（离线安装）
wget url            -- 下载指定地址的文件，如wget https://dldir1.qq.com/qqfile/qq/
                    TIM2.2.5/20871/TIM2.2.5.exe 是下载TIM的安装包，通常wget命令都需
                    要先安装才行，只有ubutu是自带的
rpm -ivh package    -- 安装软件（手动安装），如rpm -ivh jdk1.7-linux-i586.rpm
rpm -e --nodeps     -- 卸载软件
rpm -qa|grep xx     -- 查询是否已安装xx软件，如rpm -qa|grep jdk

自动安装：
yum install package     -- 自动安装指定程序
yum update package      -- 更新，升级
yum remove package      -- 卸载程序
### 1.9、进程的查杀
查进程：
ps      -- 查询系统主进程
ps -ef  --查询系统运行的所有进程
ps -ef|grep xx  -- 查询与xx相关的进程

杀进程：就是关闭相关应用程序
kill -9 xx  -- 强制杀死（终止）xx进程，xx指的是PID（进程编号，是一串数字）
### 1.10、shell脚本执行
shell脚本，指的是linux编写的程序脚本，一般保存下来的文件是.sh格式，如java的文件是.java，python的文件是.py
./脚本名.sh        -- 执行shell脚本，需要进入文件所在目录
sh 脚本名.sh       -- 也是执行shell脚本，如sh /usr/tomcat/bin/startup.sh是启动tomcat
### 1.11、文件权限管理
使用ll命令查看文件详情时，前面一段类似于-rw-r--r--这种描述，
第一个字符如果是‘d’表示这是一个目录，若是‘-’表示这是一个文件（目录以外的任何东西）
之后的字符共9个，每3个一组，格式都遵照rwx进行排列的，
第一组表示当前登录用户（u）对该文件所有的权限，
第二组表示创建这个文件的用户所在用户组（g）的权限，
第三组表示文件所有者（创建者，o）的权限。
r   -- 读取，只读  read      权限值4
w   -- 写入，编辑  write     权限值2
x   -- 执行，运行  excute    权限值1
所以一个文件权限值是由这3组rwx的权限组合相加，最小为000，最大777

chmod 权限值 文件名           -- 修改文件/目录的权限
chmod -u rwx file           -- 将当前登录用户对该文件的权限设置为rwx
## 2、Linux服务器搭建（java web Server）
### 2.1、配置java环境
#### 2.1.1、配置Jdk
1.使用ftp软件（xftp为例）上传jdk的安装文件（jdk_xxx_xxx.rpm）
2.安装jdk文件，如rpm -ivh jdk1.7-linux-i586.rpm
3.修改环境变量配置
找到/etc目录下的profile文件，进行编辑，即vi /etc/profile，加入环境变量代码
```
JAVA_HOME=/usr/java/jdk1.8.0_121
JRE_HOME=/usr/java/jdk1.8.0_121/jre
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
export JAVA_HOME JRE_HOME PATH CLASSPATH
```
这段代码加在倒数第四行的done下方
4.返回linux命令行输入java -version检测配置结构和jdk版本
#### 2.1.2、配置tomcat
1.同样上传Apache-tomcat的压缩包
2.解压
3.修改防火墙文件，即vi /etc/sysconfig/iptables
4.在文件中的COMMIT前面加入以下代码
    -A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT
5.重启防火墙相关服务，service iptables restart，使tomcat配置生效

如何启动tomcat？
    进入tomcat的bin目录
    执行./startup.sh 或sh startup.sh命令启动tomcat
#### 2.1.3、安装MySQL
自动安装
使用命令yum install mysql-server

手动安装
1.将mysql的server、client、devel三个安装包上传到linux服务器中
2.逐一对server、client、devel三个安装包进行依次安装
    如：rpm -ivh MySQL-server-5.5.55-1.el6.i686.rpm --nodeps --force
3.启动mysql服务
    service mysql start
4.修改mysql的root密码
    进入mysql（直接在命令行输入mysql，回车即可）
    切换到mysql数据库（use mysql;）
    修改user表中的root帐户密码（update user set host='%',password='123456' where user='root';）
    删除host未修改为%的root帐户（delete from user where not password='123456';）
5.配置远程访问权限
    GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;
    刷新权限
    FLUSH PRIVILEGES;
## 3、linux服务器代码部署
1.查杀tomcat进程
2.将代码的war包上传到tomcat下的webapps目录下
    如果开发人员没有编译成war包，一般都需要备份原来的代码包，也就是要返回到webapps目录，使用tar命令对原项目代码进行备份
3.重新启动tomcat（到bin目录下执行./startup.sh）
4.检查新代码中是否有需要修改的配置文件，如jdbc，系统相关位置配置等，若需要改项目内容，在修改后，还需要重启tomcat（即查杀tomcat后再次启动）

http://192.168.3.130:8080/
安装jdk
rpm -ivh jdk1.8u121-linux-i586.rpm
卸载jdk 
rpm -e --nodeps jdk1.8.0_121-1.8.0_121-fcs.i586

进入tomcat的bin目录下
cd /usr/local/apache-tomcat-7.0.70/bin
启动Tomcat
sh startup.sh
关闭Tomcat
sh shutdown.sh
查看安装的jdk：
rpm -qa|grep jdk 

可能看到如下类似的信息： 

jdk-1.6.0_22-fcs 

卸载： 

rpm -e --nodeps jdk-1.6.0_22-fcs 

rpm -e --nodeps java-1.8.0-openjdk-headless-1.8.0.222.b10-0.el6_10.x86_64

rpm -e --nodeps java-1.8.0-openjdk-devel-1.8.0.222.b10-0.el6_10.x86_64

rpm -e --nodeps java-1.8.0-openjdk-1.8.0.222.b10-0.el6_10.x86_64

