---
layout: post
category: "javascript"
title: "原生javascript中的XMLHttpRequest的使用(AJAX)"
tags: ["javascript","ajax"]
---
之前一直是使用jQuery中的ajax,不需要考虑各种兼容性,用起来也非常简单,其实原生的也不复杂,原理都一样嘛.

####根据浏览器类型获取XHR
- window.XMLHttpRequest
- window.ActiveXObject

```javascript
	var xmlhttp = null;
	if(window.XMLHttpRequest){
		xmlhttp = new XMLHttpRequest();	//现代浏览器获取的方式
	}
	else if(window.ActiveXObject){
		xmlhttp = new ActiveXObject("Microsoft.XMLhttp");	//IE6以下的浏览器获取方式
	}
```

####获取XHR之后开始链接
- xmlhttp.open();
- xmlhttp.send();
- xmlhttp.onreadystatechange

```javascript
	if(xmlhttp!=null){
		xmlhttp.open("GET", url, true);	//GET是传输方式(还有POST),url是传输地址,true是确认使用异步
		xmlhttp.send(null);	//向服务器发送的数据,没有则填null
		xmlhttp.onreadystatechange = stateChange;	//完成后状态返回
	}
	else {
		console.log("浏览器不支持XHR");
	}
	function stateChange(){
		if(xmlhttp.readyState == 4){
			if(xmlhttp.status == 200){
				//执行到这里说明成功了, 可以返回数据了
				console.log(xmlhttp.responseText);
			}
			else {
				//出错后的返回信息
				console.log(xmlhttp.statusText);
			}
		}
	}
```

以后还是能用原生javascript尽量用原生,效率高,提高学习能力.