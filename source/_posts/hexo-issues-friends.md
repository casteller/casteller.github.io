---
title: Hexo之volantis主题从Gitee Issues动态加载友链
author: MZ-ZONE
top: false
cover: true
toc: true
mathjax: false
tags:
  - volantis
  - Issues
  - Hexo
categories:
  - Hexo
date: 2020-10-20 17:35:53
img: 
headimg: https://7.dusays.com/2020/10/20/e15d43c877d22.png
coverImg:
password:
summary:
---
{% noteblock idea %}
友链对于博客来说是非常有必要的，交换友链就像交朋友一样，朋友会给你的博客带来流量，你也会给朋友送去流量，所以这对大家都是有好处的，没有谁不愿意交换的。
{% endnoteblock %}
在了解issues方式添加友链之前，我一直是添加的静态数据源，每次新增友链都需要自己添加并重新部署，感觉很麻烦。这篇文章主要针对volantis主题讲解如何使用issues标签获取json数据并解析生成html添加到页面中。其实volantis主题已经集成了此功能，但如何使用并没有做详细的阐述，于是热心的我又开始水文工作了。
<!-- more -->
<font size=6 color='orange'>🌻设置教程</font>


🍇**第一步：新建友链页面，创建页面md文件**
``` 
---
layout: friends # 必须
title: 我的朋友们 # 可选，这是友链页的标题
---
这里写友链上方的内容。
<!-- more -->
这里可以写友链页面下方的文字备注，例如自己的友链规范、示例等。
```
🍈**第二步：在主题配置文件中开启Issue功能：**
``` 
 issues:
   enable: true
   js:
```    
🍉**第三步：新建gitee仓库，创建Issues模板（新建时勾选使用Issue模板文件初始化仓库），友链Issue内容中需要有一段满足JSON格式的代码块，如下：**
```json
{
    "title": "",
    "avatar": "",
    "screenshot": "",
    "url": "",
    "description": ""
}
```
{% note info, 通过issue方式发布内容可以支持script脚本，为了安全起见，最好设置一个限制，例如用标签来激活labels=active或者只对自己发布的有效，可以在解析数据的时候过滤掉 script 标签。这样添加友链的方式就变成了：对方提 Issue ，自己审核，然后添加active标签，然后刷新网页就生效了。更新友链内容也变得十分方便，Issue 的创建者拥有修改和关闭的权限。%}
**{% span red ,所以我们需要给Issue模板增加active标签 %}**
![image](https://7.dusays.com/2020/10/20/8f53932160e2b.png)
**🍊第四步：在友链页面的md文件中添加Issue标签：**
```
{% issues sites | api=https://gitee.com/api/v5/repos/用户名/仓库名/issues?sort=created&direction=asc&labels=active&state=open&page=1&per_page=100 %}
```
{% note warning, 注意将api中的用户名和仓库名改成自己的 %}
除此之外你还可以给友链增加分组，对应Issue模板为：
```
{
    "title": "",
    "avatar": "",
    "screenshot": "",
    "url": "",
    "description": "",
    "group": "" #友链分组
}
```
对应的Issue标签格式如下：
```
{% issues sites | api=https://gitee.com/api/v5/repos/castiele/friends/issues?sort=created&direction=asc&labels=active&state=open&page=1&per_page=100 | group=group:技术大佬,朋友们 %}
```
我这里设置了两个分组：技术大佬和朋友们，效果如图：
![image](https://7.dusays.com/2020/10/20/3110cda278a26.png)

至此，所有的配置基本就完成了，小伙伴们可以自己先增加一个Issue测试一下，注意增加Issue后需添加active标签才会生效。
本文参考文章： [volantis官方文档](https://volantis.js.org/page-settings/layout/)      [静态博客使用 Issues API 发布动态、友链、书签](https://xaoxuu.com/blog/2020-08-23-issues-api/)



 

