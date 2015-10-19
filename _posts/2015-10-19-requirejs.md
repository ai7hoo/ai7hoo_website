---
layout: post
category: "javascript"
title: "js模块化管理requireJS"
tags: ["javascript","requirejs","模块化"]
---
项目大了，js的管理就成了问题，开始考虑模块化的开发，近期正好开始使用一个项目用来测试，选择了 `requirejs` .

#### index.html 载入 requirejs 文件

```html
<!--index.html-->
<script data-main="js/main.js" src="js/require.js"></script>
```

#### main.js 配置文件

```javascript
//main.js
requirejs.config({
	//配置js基目录
	baseUrl:'js',
	//配置各个js模块的位置
	path: {
		app:'../app'
	}
});

requirejs(['jquery','canvas','myModule'],function($,canvas,myModule){
	//jquery, canvas, myModule 模块现在都可以运行了。
	$("body").css("backgroundColor","red");
});
```

#### 定义自己的模块
一个磁盘文件应该只定义 1 个模块。多个模块可以使用内置优化工具将其组织打包。


```javascript
//myModule

//简单的值
//如果一个模块仅含值对，没有任何依赖，则在define()中定义这些值对就好了：
define({
	color:'red',
	size:'unisize'
});

//函数式定义
//如果一个模块没有任何依赖，但需要一个做setup工作的函数，则在define()中定义该函数，并将其传给define()：
define(function(){
	return {
		color:'red',
		size:'unisize'
	};
});

//存在依赖的函数式定义
//如果模块存在依赖：则第一个参数是依赖的名称数组；第二个参数是函数，在模块的所有依赖加载完毕后，该函数会被调用来定义该模块，因此该模块应该返回一个定义了本模块的object。依赖关系会以参数的形式注入到该函数上，参数列表与依赖名称列表一一对应。
define(['./cart','./inventory'],function(cart,inventory){
	return {
		color:'red',
		size:'unisize',
		addToCart:function(){
			inventory.decrement(this);
			cart.add(this);
		}
	};
});

//将模块定义为函数
//对模块的返回值类型并没有强制为一定是个object，任何函数的返回值都是允许的。此处是一个返回了函数的模块定义：
define(['./cart','./inventory'],function(cart,inventory){
	function (cart,inventory){
		return function (title){
			return title?(window.title = title):inventory.storeName + ' ' + cart.name;
		};
	}
});
```
