---
layout: post
category: "javascript"
title: "babel 解析和配置"
tags: ["babel", "es6"]
---

## babel 是什么
babel 是下一代javascript语法的编译器

作为前端开发，由于浏览器的版本和兼容性问题，很多javascript的新的方法都不能用，等到可以大胆使用的时候，肯能已经过去好几年了。babel就是为此而生的。他可以让广大前端放心大胆的使用大部分的javascript的新的标准的方法。然后编译成兼容绝大多数主流浏览器的代码。

在升级到babel6.x版本之后，所有的插件都是可插拔的，这也就意味着你安装了babel之后，是不能工作的，需要配置队形的.babelrc文件才能发挥完成的作用。下面就开始对babel的presets和plugins配置做一个简单的解析。
所有配置根据[官方文档](https://babeljs.io/docs/plugins/)提供，更新时间：2016-12-05

## 预设(presets)
使用的时候需要安装队形的插件，对应的babel-preset-xxx,例如下面的配置，需要 `npm install babel-preset-es2015`
``` javascript
{
  "presets": ["es2015"]
}
```
***env***
``` javascript
{
  "presets": ["env": options]
}
```
最近新增的一个选项，有以下options选择。

***targets: {[string]: number}, 默认{}***
需要支持的环境，可选如：chrome,edge,firefox,safari,ie,ios,node,甚至可以置顶版本，如node:6.5。也使用node:current代表使用当前的版本。

***browsers: Array|string, 默认[]***
浏览器列表，使用的是browserslist,可选例如：last2 versions, > 5%。

***loose:boolean,默认false***
是否使用宽松模式，如果设置为trun,plugins里的插件如果允许，都会采用宽松模式。

***debug: boolean,默认false***
编译是否会去掉console.log。

***whitelist:Array,默认[]***
设置一直引入的plugins列表

***es2015/es2016/es2017/latest***
## 插件(plugins)
其实看来上门的应该也明白了，presets,也就是一堆plugins的预设，起到方便的作用。如果不采用presets，完全可以单独引入某个功能，比如以下的设置就会引入编译箭头函数的功能。
那么还有一些方法是presets中不提供的，这时候就需要单独引入了，介绍几个常见的插件。
### transform-runtime
该插件最大的作用有以下几点：
- 解决编译中产生的重复的工具函数，减小代码体积
- 非实例方法的poly-fill，如Object.assign，但是实例方法不支持，如`"foobar".includes("foo")`,这时候需要单独引入babel-polyfill
- 更多细节参见[文档](https://babeljs.io/docs/plugins/transform-runtime/)

``` javascript
{
  "plugins": ["tranform-runtime": options]
}
```
### transform-remove-console
使用这个插件，编译后的代码都会移除`console.*`，妈妈再也不用担心线上代码有多余的console.log了。当然很多时候，我们如果使用webpack，会在webpack中配置。
这也告诉我们，babel不仅仅是编译代码的工具，还能对代码进行压缩，也许有一天，你不再需要代码压缩的插件了，因为你有了babel。
## 自定义预设或者插件
babel支持自定义的预设（presets）或插件（plugins），如果你的插件在np0m上，可以直接采用这种方式`"plugins": ["babel-plugin-myPlugin"]`，当然，也可以使用缩写，它和`"plugins": ["myPlugin"]`是等价的。此外，你还可以采用本地的相对路径引入插件，比如`"plugins": ["./node_modules/path/plugin"]`。
presets同理
## plugins/presets排序
也许你会问，或者你没注意到，我帮你问了，plugins和presets编译，或许有相同的功能，或者有联系的功能，按照怎么的顺序进行编译？答案是会按照一定的顺序。
- 具体而言，plugins优于presets进行编译
- plugins按照数组的index增序（从数组第一个到最后一个）进行编译。
- presets按照数组的index倒序（从数组的最后一个到第一个）进行编译。因为作者认为大部分会把presets写成`["es3015", "stage-0"]`。具体细节可以看[这里](https://github.com/babel/notes/blob/master/2016-08/august-01.md#potential-api-changes-for-traversal)

## 其他
comments 可以去除脚本中的注释，false 则不显示备注
``` javascript
{
	"comments": false
}
```

## 总结
这是我写了半天发现比较推荐的配置（真的是太简单了，还花了这么久去看文档）。强烈推荐使用 `transform-runtime`。

``` javascript
{
  "parsets": ["es2015", "stage-0"],
  "plugins": ["transform-runtime"]
}
```

当然，如果你的项目需要react或者flow这些语法的编译，请在preset里键入队形的值即可。如果你需要非实例方法`"foobar".includes("foo")`之类的方法，按需引入babel-polyfill。
本文来源 [韩小平的博客](https://excaliburhan.com/post/babel-preset-and-plugins.html)