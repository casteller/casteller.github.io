---
title: hexo博客之volantis主题添加上浮气泡特效
author: MZ-ZONE
top: false
cover: true
toc: true
mathjax: false
date: 2020-10-19 10:02:23
img:
headimg: https://7.dusays.com/2020/10/19/036866ed88ed1.png
coverImg:
password:
summary:
tags:
   - [volantis]
   - Hexo
categories:
   - [Hexo]
---
{% noteblock idea %}
在群友黑石大佬的主页：**www.heson10.com**，看到了上升气泡的特效，觉得很赞，于是乎，搬运工又来活了。
{% endnoteblock %}
<!-- more -->
**💎先上我搬运之后的效果图：**
![image](https://hexo-1301734500.cos.ap-chengdu.myqcloud.com/archives/canvas%E6%B0%94%E6%B3%A1.gif)
**💡下面开始介绍添加方法：**
- 在{% span red, Blog\themes\hexo-theme-volantis-master\source\js\app.js %}文件中添加以下代码（其中气泡数量，大小，上升速度等可根据需要自行调整）：

```java
(function() {
	var canvas, ctx, width, height, bubbles, animateHeader = true;
	initHeader();
	function initHeader() {
		canvas = document.getElementById('header_canvas');
		window_resize();
		ctx = canvas.getContext('2d');
		//建立泡泡
		bubbles = [];
		var num = width * 0.15;//气泡数量
		for (var i = 0; i < num; i++) {
			var c = new Bubble();
			bubbles.push(c);
		}
		animate();
	}
	function animate() {
		if (animateHeader) {
			ctx.clearRect(0, 0, width, height);
			for (var i in bubbles) {
				bubbles[i].draw();
			}
		}
		requestAnimationFrame(animate);
	}
	function window_resize() {
		//canvas铺满窗口
		width = window.innerWidth;
		height = window.innerHeight;

		// //如果需要铺满内容可以换下面这个
		// var panel = document.getElementById('header_canvas');
		// width=panel.offsetWidth;
		// height=panel.offsetHeight;

		canvas.width = width;
		canvas.height = height;
	}
	window.onresize = function(){
		window_resize();
	}
	function Bubble() {
		var _this = this;
		(function() {
			_this.pos = {};
			init();
		})();
		function init() {
			_this.pos.x = Math.random() * width;
			_this.pos.y = height + Math.random() * 100;
			_this.alpha = 0.1 + Math.random() * 0.5;//气泡透明度
			_this.alpha_change = 0.0002 + Math.random() * 0.0005;//气泡透明度变化速度
			_this.scale = 0.2 + Math.random() * 0.1;//气泡大小
			_this.scale_change = Math.random() * 0.001;//气泡大小变化速度
			_this.speed = 0.1 + Math.random() * 0.9;//气泡上升速度
		}
		//气泡
		this.draw = function() {
			if (_this.alpha <= 0) {
				init();
			}
			_this.pos.y -= _this.speed;
			_this.alpha -= _this.alpha_change;
			_this.scale += _this.scale_change;
			ctx.beginPath();
			ctx.arc(_this.pos.x, _this.pos.y, _this.scale * 10, 0, 2 * Math.PI, false);
			ctx.fillStyle = 'rgba(255,255,255,' + _this.alpha + ')';
			ctx.fill();
		};
	}
})();
```


- 然后在{% span red, Blog\themes\hexo-theme-volantis-master\layout\_partial\cover.ejs %}文件中加入以下代码：

```html
<canvas id="header_canvas"style="position:absolute;bottom:0;z-index: 1;width:1366;height:610"></canvas>
```

![image](https://7.dusays.com/2020/10/19/92a044fb65df3.png)
- 到这一步在首页其实就可以看到了，但是你会发现底部的气泡会浮于侧边栏和文章头图上方
![image](https://7.dusays.com/2020/10/19/f49d399827814.png)
- 这时我们找到侧边栏css文件{% span red, Blog\themes\hexo-theme-volantis-master\source\css\_layout\sidebar.styl %}，找到l_side增加z-index属性：

``` css
.l_side
  width: $sidebar
  float: right
  position: relative
  display: flex
  flex-direction: column
  +z-index : 2
```
- 然后找到文章列表的css文件{% span red, Blog\themes\hexo-theme-volantis-master\source\css\_layout\main.styl %}，找到l_main增加z-index属性：

```css
.l_main
  width: "calc(100% - 1 * %s)" % $sidebar
  @media screen and (max-width: $device-tablet)
    width: 100%
  padding-left: $gap
  +z-index: 2;
```
{% noteblock idea %}
注：z-index属性值只要比1大就行，因为刚刚canvas标签的z-index我们设置的1。
{% endnoteblock %}

最后hexo一键三连，快部署上去让大伙儿看看吧

