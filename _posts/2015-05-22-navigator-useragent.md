---
layout: post
category: "javascript"
title: "判断浏览器类型"
tags: ["javascript","userAgent"]
---
浏览器的类型判断可以用`navigator`,它有个属性是`userAgent`,可以用在这里,例如：

```javascript
var u_agent = navigator.userAgent;
if( u_agent.indexOf("Firefox") > -1 ){
	console.log('Firefox');
}
else if( u_agent.indexOf("Chrome") > -1 ){
	console.log('Chrome');
}
else if( u_agent.indexOf("MSIE") > -1 ){
	console.log('IE(8-10)');
}
else {
	console.log('Other...');
}
```