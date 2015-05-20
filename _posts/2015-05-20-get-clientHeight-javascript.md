---
layout: post
category: "javascript"
title: "javascript获取浏览器当前视图下的尺寸"
tags: ["javascript"]
---
之前了解到很多种有关获取屏幕尺寸,文档尺寸,显示区域尺寸的方式,越多越乱了.有的但是关于屏幕分辨率的,有的是关于工作区的,还有关于文档dom的高度的.记一下以便更好地理解.

#### 获取当前显示窗口尺寸
当前显示窗口就是指的浏览器中显示网页内容的尺寸,不包含工具条,状态栏,书签栏,滚动条等.这个我用的比较多的一个.比如之前没有media的时候用来js来获取浏览器尺寸以便使用响应式.

```javascript
	var hl = document.documentElement.clientHeight();
	var wl = document.documentElement.clientWidth();
```

#### 获取屏幕分辨率的尺寸
当前屏幕的分辨率,显示器分辨率,如果使用移动设备并且设置了 `<meta name="viewport" content="width=device-width, initial-scale=1.0">` 属性那么分辨率可能就是其他的如,640*360等,经过缩放的分辨率.

```javascript
	var hl = window.screen.height;
	var wl = window.screen.width;

	//这个是获取的去除了windows任务栏的工作区宽高
	var hl = window.screen.availHeight;
	var wl = window.screen.availWidth;
```

#### 获取整个文档的高度宽度尺寸
一般是指的整个body可见区域的宽高尺寸	

```javascript
	//网页可见区域的宽高
	var hl = document.body.clientHeight;
	var wl = document.body.clientWidth;

	//网易可见区域的宽高(包括边线)
	var hl = document.body.offsetHeight;
	var wl = document.body.offsetWidth;

	//网页正文全文高
	var hl = document.body.scrollHeight;
	var wl = document.body.scrollWidth;
```


###一张示意图
赶脚好乱的哦.这类属性没有统一,还是用JQuery比较好了.有空再继续研究.

![javascript获取浏览器当前视图下的尺寸](/images/o_client-offset-scroll.jpg "javascript获取浏览器当前视图下的尺寸")