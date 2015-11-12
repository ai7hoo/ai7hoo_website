---
layout: post
category: "javascript"
title: "面向切面编程学习"
tags: ["javascript","AOP"]
---

在不影响原来的程序逻辑的情况下需要做其他的例如统计或其他的回调处理的时候，会用到 AOP 的编程方式。

-------------------------------------

比如需要统计所有的函数 function 的执行时间的时候：
```javascript
function test(){
	//alert(2);
	return 'aaa';
}
```

如果把代码写在内部会很容易影响业务逻辑，或者说污染变量，这个时候，就需要使用 AOP 来实现统计。可以从 function 原型上去做些文章。

```javascript
Function.prototype.before = function(fn){
	var __self = this;
	return function(){
		fn.apply(__self,arguments);
		return __self.apply(__self,arguments);
	}
}

Function.prototype.after = function(fn){
	var __self = this;
	return function(){
		var result = __self.apply(__self,arguments);
		if(result == false){
			return false;
		}
		fn.apply(this,arguments);
		return result;
	}
}

test.before(function(){
	console.time('a');
}).after(function(){
	console.timeEnd('a');
})();

```