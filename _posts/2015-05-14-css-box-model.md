---
layout: post
category: "css"
title: "css3盒模型"
tags: ["css"]
---
css3的盒模型有段时间没看居然有些生疏了，一直用框架，也忘记了原理。盒模型是CSS3新增的属性，可以把盒模型以标准模式显示（content-box），或者以传统IE6以下（不含IE6）的模式显示（border-box）.

#### 标准盒模型content
现代浏览器的标准盒模型

``` CSS
	div {
		box-sizing: content-box;
	}
```

#### 传统模式border
传统IE6以下（不含IE6）的方式

``` CSS
	div {
		box-sizing: border-box;
	}
```

图片示例

![box-model-layout](/box-model-layout.png "box-model-layout")