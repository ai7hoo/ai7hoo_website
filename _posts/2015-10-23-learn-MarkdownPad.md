---
layout: post
category: "other"
title: "learn-MarkdownPad"
tags: ["Markdown"]
---

## Welcome to MarkdownPad 2 ##

**MarkdownPad** is a full-featured Markdown editor for Windows.

### Built exclusively for Markdown ###

Enjoy first-class Markdown support with easy access to  Markdown syntax and convenient keyboard shortcuts.

Give them a try:

- **Bold** (`Ctrl+B`) and *Italic* (`Ctrl+I`)
- Quotes (`Ctrl+Q`)
- Code blocks (`Ctrl+K`)
- Headings 1, 2, 3 (`Ctrl+1`, `Ctrl+2`, `Ctrl+3`)
- Lists (`Ctrl+U` and `Ctrl+Shift+O`)

### See your changes instantly with LivePreview ###

Don't guess if your [hyperlink syntax](http://markdownpad.com) is correct; LivePreview will show you exactly what your document looks like every time you press a key.

### Make it your own ###

Fonts, color schemes, layouts and stylesheets are all 100% customizable so you can turn MarkdownPad into your perfect editor.

### A robust editor for advanced Markdown users ###

MarkdownPad supports multiple Markdown processing engines, including standard Markdown, Markdown Extra (with Table support) and GitHub Flavored Markdown.

With a tabbed document interface, PDF export, a built-in image uploader, session management, spell check, auto-save, syntax highlighting and a built-in CSS management interface, there's no limit to what you can do with MarkdownPad.

### Javascript code

``` javascript
window.onload = function(){
	var getInfo = new Vue({
		el:'#userInfo',
		data:{
			items:[]
		},
		methods:{
			onCclick:function(id){
				//do something...
			}
		}
	});

	$.ajax({
		url:SERVER_IP+'/front/get_user_info',
		type:'get',
		dataType:'json',
		beforeSend:function(){},
		success:function(result){
			getInfo.items = result.data;
		},
		error:function(){}
	});
};
```

### HTML code

```html
<script src="/js/jquery.js"></script>
<script src="/js/vue.min.js"></script>
...
<div class="user">
	<template id="userInfo" v-repeat="item in items">
		<div class="{{item.isVip?'isVip':''}}" v-text="item.name" data-userId="{{item.userId}}" v-on="click:onClick(item.userId)" ></div>
	</template>
</div>
```