---
layout: post
category: "javascript"
title: "Vue.js 简单介绍"
tags: ["javascript","vue"]
---

数据驱动的组件，为现代化的 Web 界面而生。已经使用 Vue.js 两三个月了。实际项目中也有三四个使用的。各种数据绑定，组件化，路由功能用起来非常方便。 

以下先简单记一下 ...


#### 安装

NPM 安装：

```` cmd
npm install vue
````

Bower 安装

```` cmd
bower install vue
````

符合规范，可直接用作AMD模块


#### Hello world

HTML

```` HTML
<div id="app" v-text="message"></div>
````

javascript

```` javascript
new Vue({
	data:{
		message:'Hello World!'
	}
});
````
2016/3/16 14:37:32 