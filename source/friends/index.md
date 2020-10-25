---
layout: friends # 必须
title: # 可选，这是友链页的标题
sidebar: [blogger, category, tagcloud, qrcode,webinfo]
cover: true
---
<br>
<br>
<center>
<span class="p large red">👦我</span>
<span class="p large yellow">的</span>
<span class="p large green">好</span>
<span class="p large blue">友</span>
<span class="p large cyan">们</span>
</center>
<!-- more -->
<!--这里可以写友链页面下方的文字备注，例如自己的友链规范、示例等。-->
{% issues sites | api=https://gitee.com/api/v5/repos/castiele/friends/issues?sort=created&direction=asc&labels=active&state=open&page=1&per_page=100 | group=group:技术大佬,朋友们 %}
{% noteblock idea %}
欢迎交换友链！{% span  red, 先 %}{% span  yellow, 友 %}{% span  green, 后 %}{% span  cyan, 链 %}
{% endnoteblock %}

{% tabs tab-id %}

<!-- tab 📜友链申请流程 -->
{% timenode 第一步：先将本站链接添加至贵站 %}
> * 名称：木子の博客
> * 链接：https://www.mz-zone.cn
> * 头像：https://7.dusays.com/2020/10/19/b246230298bf0.png
> * 网站截图：https://7.dusays.com/2020/10/19/9f3e79b445a84.png
> * 描述：积水成河，积土成山！
{% endtimenode %}
{% timenode 第二步：前往Gitee，新建[Issues](https://gitee.com/castiele/friends/issues)（👈点我）按照格式填写并提交 %}
```json
{
    "title": "",
    "avatar": "",
    "screenshot": "",
    "url": "",
    "description": "",
    "group": "朋友们"
}
```
为提高图片加载速度，建议优化头像和截图：
1. 打开 [压缩图](https://www.yasuotu.com/) 上传自己的截图，将图片大小压缩到 1Mb以下。
2. 将压缩后的图片上传到自己搭建的图床、[去不图床](https://7bu.top/) 等，并使用此图片链接作为截图。
{% endtimenode %}
{% timenode 第三步：下方评论区留言，等待博主审核 %}
> * 评论区记得填写QQ邮箱，博主会收到微信及邮件通知，待审核通过后刷新本页面即可显示
{% endtimenode %}

<!-- endtab -->

<!-- tab 📙友链申请须知 -->
{% checkbox checked blue, 请确保您的博客站点能够正常访问，禁止死链 %}
{% checkbox checked cyan, 原则上只接收博客类网站友链，资源站、视频站等一切非博客类网站不予交换 %}
{% checkbox checked red, 页面保证无繁杂广告推广 %}
<!-- endtab -->

{% endtabs %}
