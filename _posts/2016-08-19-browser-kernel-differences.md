---
layout: post
category: "web"
title: "不同浏览器内核差异"
tags: ["web"]
---

浏览器内核主要是渲染引擎和javascript引擎,负责解释并渲染网页。


#### PC端浏览器内核

1. Trident

	IE使用的内核，一直到IE9.
2. Gecko

	Netscape6开始使用的内核，后来被firefox(火狐)也采用的内核。
3. Presto

	Opera浏览器使用的内核
4. Webkit

	首先是苹果在Safari上使用的内核，后来google也在chrome中使用的内核

#### 移动端浏览器内核

手机端Trident主要在微软的WP操作系统中使用的内核，市场占有率少。占有率最高的为webkit，主要是在Android原生浏览器和IOS中Safari采用的内核。

当然内核并无PC端和移动端之分。


## 另一种浏览器内核说明
### 一 排版引擎
英文叫做：Rendering Engine，中文翻译很多，排版引擎、解释引擎、渲染引擎，现在流行称为浏览器内核。

Rendering Engine，顾名思义，就是用来渲染网页内容的，将网页的内容和排版代码转换为可视的页面。因为是排版，所以肯定会排版错位等问题。为什么会排版错位呢？有的是由于网站本身编写不规范，有的是由于浏览器本身的渲染不标准。

1. Trident
2. Gecko
3. KHTML
4. WebKit
5. Chromium
6. Presto

### 二 javascript 引擎
说完了排版引擎，接下来说说JavaScript引擎。顾名思义，JavaScript引擎就是用来渲染JavaScript的。

为什么要单独拿出来说呢？因为它涉及到跑分。经常看见很多文章在报道说哪个浏览器更快，其实大部分说的就是JavaScript的渲染速度，而不是页面的载入速度。在网速许可的情况下，其实各个浏览器的页面载入速度差别不大（Opera逊色一些）。那是不是说对比JavaScript的渲染速度其实没有意义？也不是这么说，因为现在JavaScript在页面中的比重会越来越大，越来越多的动态页面开始大量借助JavaScript，比如现在主流的SNS、邮箱、网页游戏，所以JavaScript的渲染速度也是一个很重要的指标。

JavaScript的渲染速度越快，动态页面的展示也越快。Opera在JavaScript引擎的跑分上面一直都是很牛逼的，一般来说最新测试版之间PK，Opera基本都会夺冠。

1. Chakra

	查克拉，IE9启用的新的JavaScript引擎。
2. SpiderMonkey/TraceMonkey/JaegerMonkey
	
	SpiderMonkey应用在Mozilla Firefox 1.0-3.0，TraceMonkey应用在Mozilla Firefox 3.5-3.6版本，JaegerMonkey应用在Mozilla Firefox 4.0及后续的版本。
3. V8

	应用于Chrome、傲游3。
4. Nitro

	应用于Safari 4及后续的版本。
5. Linear A/Linear B/Futhark/Carakan

	Linear A应用于Opera 4.0-6.1版本，Linear B应用于Opera 7.0～9.2版本，Futhark应用于Opera 9.5-10.2版本，Carakan应用于Opera 10.5及后续的版本。
6. KJS

	KHTML对应的JavaScript引擎。

### 浏览器渲染原理
Web页面运行在各种各样的浏览器当中，浏览器载入、渲染页面的速度直接影响着用户体验简单地说，页面渲染就是浏览器将html代码根据CSS定义的规则显示在浏览器窗口中的这个过程。

**先来大致了解一下浏览器都是怎么干活的：**

1. 用户输入网址（假设是个html页面，并且是第一次访问），浏览器向服务器发出请求，服务器返回html文件； 　　

2. 浏览器开始载入html代码，发现<head>标签内有一个<link>标签引用外部CSS文件； 　　

3. 浏览器又发出CSS文件的请求，服务器返回这个CSS文件； 　　

4. 浏览器继续载入html中<body>部分的代码，并且CSS文件已经拿到手了，可以开始渲染页面了； 　　

5. 浏览器在代码中发现一个<img>标签引用了一张图片，向服务器发出请求。此时浏览器不会等到图片下载完，而是继续渲染后面的代码； 　　

6. 服务器返回图片文件，由于图片占用了一定面积，影响了后面段落的排布，因此浏览器需要回过头来重新渲染这部分代码； 　　

7. 浏览器发现了一个包含一行Javascript代码的<script>标签，赶快运行它； 　　

8. Javascript脚本执行了这条语句，它命令浏览器隐藏掉代码中的某个（style.display=”none”）。杯具啊，突然就少了这么一个元素，浏览器不得不重新渲染这部分代码； 　　

9. 终于等到了</html>的到来，浏览器泪流满面…… 　　
10. 等等，还没完，用户点了一下界面中的“换肤”按钮，Javascript让浏览器换了一下<link>标签的CSS路径； 　　
11. 浏览器召集了在座的各位