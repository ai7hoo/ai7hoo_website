---
layout: post
category: "javascript"
title: "javascript中的正则表达式"
tags: ["javascript"]
---
正则表达式看起来跟乱码似得，现在又理了一下

#### 在js中正则的应用
1.内容替换
2.表单验证
3.搜索匹配

#### 新建正则表达式

```javascript
	//第一种方式
	var pattern = new RegExp("box","igm");	//第一个参数是匹配内容，第二个参数是可选参数，i忽略大小写,g是全局匹配,m是忽略换行
	var pattern = /box/igm;
```

#### 方法

```javascript
	pattern.test(str);	//检测str字符串是否匹配pattern,返回布尔值
	pattern.exec(str);	//通过检测str字符串里面是否匹配pattern,返回一组数组,没有匹配则返回null
```

#### 可使用正则匹配的字符串属性

```javascript
	str.match(pattern);	//返回数组,可以通过pattern.length获取数量
	str.search(pattern);	//返回位置,type number,找不到返回-1
	str.replace(pattern,'ostr');	//匹配后替换成第二个参数,开了全局可以替换所有的,否则只替换第一个
	str.split(pattern);	//按照表达式把字符串分割成数组
```