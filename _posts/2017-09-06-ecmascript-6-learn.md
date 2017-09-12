---
layout: post
category: "javascript"
title: "EcmaScript 6 学习笔记"
tags: ["es6", "ecmascript"]
---

# EcmaScript 学习指南
学习 [EcmaScript 6 入门](https://wohugb.gitbooks.io/ecmascript-6/content/)
再次跟着这本开源书籍过一遍 ES6 的内容


## 1. 简介
### ecmascript 与 javascript 的关系
ecmascript 是 javascript 语言的估计标准
javascript 是 ecmascript 的实现
前者是后者的规范，后者是前者的实现。
### ecmascript 7 新功能
- Object.observe 用来监听对象/数组的变化，一旦监听到变化就触发回调
- Multi-Threading 多线程支持
- Traits 它将是 **类** 功能的替代

## 2. let 和 const 命令
### let 命令
类似 var ，但是只在当前所在的代码块内有效，
- 拥有块级作用域，很适合for循环计数器
- let 不会发生变量提升的现象。
- 并且不能重复声明。
### const 命令
也是用来声明变量，
- 但是声明后，不能再修改。
- 并且 const 的作用域和 let 相同，也是在快内部有效。
- 也不可以重复声明

## 3. 变量的解构赋值
### 数组的解构赋值
ES6允许按照一定的方式，从数组和对象中提取值，对变量进行赋值，这称为解构.
- 左少右多，不完全解构
- 左多右少，缺少的变量赋值 undefined
- 适用于 var / let / const
- 需按照顺序排列

``` javascript
// 以前交换两个变量的值
var a = 1
var b = 2
var c = a
a = b
b =c

// ES6
var [a, b] = [1, 2]
var [a, b] = [b, a]
```
### 对象的解构赋值
不同于数组的结构赋值，
- 对象的解构赋值，不需要按照顺序排列
- 但是属性名要对应
- 可以指定变量名
- 可以指定默认值

``` javascript
var {uname, say, eot: eat, sleep = 'yes'} = {uname: 'quinn', say: function(){console.log('hi')},eat: 'food'}
console.log(uname)
say()
console.log(eat)
console.log(sleep)
```
### 解构赋值的用途
- 交换变量值

``` javascript
[x,y] = [y,x]
```
- 从函数返回多个值

``` javascript
// 返回一个数组
function test(){
  return [1,2,3]
}
var [a,b,c] = test()

// 返回一个对象
function test2(){
  return {
    foo: 1,
    bar: 2
  }
}
var {foo, bar} = test2()
```
- 函数参数的定义
- 函数参数的默认值
- 遍历Map结构
- 输入模块的置顶方法

``` javascript
// 加载模块的时候，往往需要置顶输入那些方法，解构赋值使得输入语句非常清晰
const {baseUrl} = require('config')
```

## 4. 字符串的扩展
- codePointAt()
- String.fromCodePoint()
- at()
- 字符串的 Unicode 表示法
- 正则表达式的u修饰符
- normalize()
- contains() startsWith() endsWith()
- repeat()
- 正则表达式的y修饰符
- 模版字符串

## 5. 数值的扩展
- 二进制和八进制的表示法。
	- 二进制 0b1010
	- 八进制 0o797
	- Number 扩展
		- Number.isFinite() 是否非有限大小的数字。区别与 isFinite()，会检测数据类型
		- Number.isNaN() 是否是非数字型。区别与 isNaN()
		- Number.parseInt() 等价于 parseIn()，只是移植到 Number
		- Number.parseFloat() 等价于 parseFloat(),只是移植到 Number
		- Number.isInteger() 判断是否为整数，主要 3 和 3.0 等价
		- Number.MIN_SAFE_INTEGER ES6中可准确表示的最小整数常量。
		- Number.MAX_SAFE_INTEGER ES6中可准备表示的最大整数常量。
		- Number.isSafeInteger() 判断某个整数是否在安全范围内
	- Math 扩展
		- Math.trunc() 去除一个数的小数部分，返回整数部分
		- Math.acosh()
		- Math.asinh()
		- Math.atanh()
		- Math.cbrt() 立方根
		- Math.clz32()
		- Math.cosh()
		- Math.expm1()
		- Math.fround()
		- Math.hypot()
		- Math.imul()
		- Math.log1p()
		- Math.log2()
		- Math.sign()
		- Math.tanh()

## 6. 数组的扩展
### Array.from()
用于把类似数组的对象或者可遍历的对象转换成数组，
### Array.of()
用户将一组数，转换成数组
### [].find() / [].findIndex()
find()用于找到符合条件的元素，参数是一个回调函数
findIndex()和find()类似，不过用于返回找到符合条件的元素的索引

``` javascript
[1,2,3,4].find((item, index, arr) => {
  return item > 2
})
```
### fill()
填充数组

``` javascript
['a','b','c'].fill(4)
// [4,4,]

new Array(4).fill(2)
// [2,2,2,2]

[0,1,2,3,4].fill('a', 2,3)
// [0,1,'a',3,4]
// 第二个和第三个参数指定开始和结束位置
```
### entries() keys() values()
可以用与遍历数组，区别是：
- entries 遍历键值对
- keys 遍历键名
- values 遍历键值

``` javascript
for(let index of ['a','b'].keys()) {
  console.log(index)
}
for(let value of ['a','b'].values()) {
  console.log(value)
}
for(let [index, ele] of ['a','b'].entries()) {
  console.log(index,ele)
}
```

### 数组推导
``` javascript
var a1 = [1,2,3]
var a2 = [for (i of a1) i * 3]
// a2 = [3,6,9]
```

### Array.observe() / Array.unobserve()
用于监听/取消监听数组的编号，属于ES7的一部分

## 7. 对象的扩展
### 属性的简介表示法
可以直接写入变量和函数，作为对象的属性和方法，更加简洁

``` javascript
var a = 1
var b = function(){
  console.log(2)
}
var data = {
  a,
  b,
  c: 3
}
data.b()
// 2
```
### 属性名表达式

``` javascript
var hi = 'xxxxx'
let data = {
  [hi]: 1,
  ['b'+'a'+hi]: 2
}
data = {
  xxxxx: 1,
  baxxxxx: 2
}
```

### Object.is()
比较两个值是否严格等于，可用于比较NaN

``` javascript
Object.is(+0, -0)
// false
Object.is(NaN, NaN)
// true
```
### Object.assign()
可用于将可枚举的对象属性，赋值到目标对象,多个对象参数时，如果有相同参数名那么后面的对象属性值会覆盖前面的。可用于插件组件模块，设置默认值

``` javascript
var data1 = {a: 1}
var data2 = {a: 2, b: 3}
var data3 = Object.assign({}, data1,data2)
// data3 = {a: 2,b3}
```

### proto 属性
proto属性，用于读或者设置当前对象的 prototype 对象。有了这个属性就不需要通过Object.create()来生成新对象了。

``` javascript
// ES6写法
var obj = {
  __proto__: someObj,
  method: function(){}
}

// ES5写法
var obj = Object.create(someObj)
obj.method = function(){}
```
- Object.setPrototypeOf()
方法作用与proto相同，都是用来设置一个对象的 prototype 对象
``` javascript
// 格式
Object.setPrototypeOf(object,prototype)
// 用法
var o = Object.setPrototypeOf({}, null)

// 等同于
function (obj,proto) {
  obj.__proto__ = proto
  return obj
}
```
- Object.getPrototypeOf()
该方法与 setPrototypeOf 配套使用，用于获取一个对象的 prototype 对象
Object.getPrototypeOf(obj)

### Symbol
ES6 引入一种新的原始数据类型，表示独一无二的ID，它通过 Symbol 函数生成
- 可以接受一个参数作为实例名称
- 拥有 name 属性，可用来获取
- 不能使用 new 命令来生成，因为这是一个原始类型的值，不是对象
- 不能和其他类型的值进行运算，会报错
- 但是 Symbol 类型可以转换为字符串 sym.toString()
- symbol 最大的特点就是每一个 symbol 都是不想等的，保证产生一个独一无二的值

```
let symbol = Symbol()
typeof symbol == 'symbol'

// Symbol 可接受一个字符串作为参数，用来表示Symbol实例的名称
let sym = Symbol('quinn')
sym.name == 'quinn'
```

### Proxy
proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种 ***元编程 meta programming*** 即对编程语言进行编程。
Proxy 可以理解成在目标对象之前，架设一层 ***拦截*** ，对外界对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。 Proxy 这个词的原意是代理，用在这里表示他来 ***代理某些操作***
作为构造函数，Proxy 接受两个参数，第一个是要代理的对象，第二个对象是一个设置对象，对于每一个被代理的操作，需要提供一个对应的处理函数。

``` javascript
var proxy = new  Proxy({},{
  get: function(target,property){
    if (property in target) {
      return target[property]
    }else {
      throw new Error('对象没有该属性')
    }
  }
})
console.log(proxy.username)
// 抛出错误
```
proxy 支持的拦截器
- get(target,propKey,receiver)
- defineProperty(target,propKey,propDesc)
- deleteProperty(target,propKey)
- enumberate(target)
- getOwnPropertyDescriptor(target,propKey)
- getPrototypeOf(target)
- has(target,propKey)
- isExtensible(target)
- ownKeys(target)
- preventExtensions(target)
- set(target,propKey,value,receiver)
- setPrototypeOf(target,proto)
如果对象是函数，那么还有两种额外操作可以拦截
- apply
- construct

### Object.observe() / Object.unobserve()
用于监控对象的变化。属于ES7的内容

## 8. 函数的扩展
### 函数参数的默认值
ES6之前不能为函数指定默认值，只能在函数内部通过判断参数是否为 undefined 来指定

``` javascript
// 之前的写法 1
function log1(x,y) {
  y = y || ' world'
  console.log(x,y)
}
// 之前写法 2
function log2(x,y) {
  if (y === 'undefined') {
    y = ' world'
  }
  console.log(x,y)
}
// 之前写法 3
function log3(x,y) {
  if(arguments.length === 1) {
    y = ' world'
  }
  console.log(x,y)
}
// ES6
function (x,y = ' world'){
  console.log(x,y)
}
```
### rest 参数
用于获取函数多余参数，这样就不需要使用 arguments 对象了。注意 rest参数后面不能再跟参数了，否则会报错

``` javascript
function count(first, ...values) {
  let sum = first
  for(let item in sum) {
    sum += item
  }
}
console.log(count(100, 1,2,3,4,5,6,7))
```

### 扩展运算符
相当于 rest参数的逆运算

### 箭头函数
ES6允许使用箭头 *** => *** 定义函数

``` javascript
var y = v => v
// 等同于
var y = function (v){
  return v
}
```
箭头函数有以下几个注意点：
- ***函数体内部的this对象，绑定定义时所在的对象，而不是使用时所在的对象。***
- 不可以当作构造函数，也就是说，不可以使用 new 命令，否则会报错
- 不可以使用 arguments 对象，该对象在函数提内部不存在

## 9. Set 和 Map 数据结构
### Set()
ES6提供的新的数据结构 ，类似数组，但是成员唯一，没有重复
属性和方法
- 属性
	- Set.prototype.constructor
	- Set.prototype.size
- 方法
	- add(val) 添加某个值，返回本身
	- delete(val) 删除某个值，返回布尔，表示是否删除成功
	- has(val) 判断是否有某个值，返回布尔
	- clear() 清空所有成员，没有返回值
### WeakSet
结构类似Set,也是不重复的几何，但是与Set有两个区别
- 成员只能是对象，
- WeakSet 对象都是弱引用，不可遍历

### Map
javascript 对象的键值中的键只能是使用字符串，这里使用 Map 能让对象当键名
### WeakMap
类似Map,但是只能让对象当作键名。

## Iterator 和 for...of
### Iterator
遍历器（Iterator）

``` javascript

function idMaker(array) {
  var index = 0
  return {
    next: function() {
      // return {value: index++, done: false}
      return index < array.length ? {value: index++, done: false} : {value: undefined, done: true}
    }
  }
}

var it = idMaker([1,2])
console.log(it.next().value) 、、
console.log(it.next().value)
console.log(it.next().value)
```
### for...of

## Generator 函数
所谓Generator,有多种理解方式，。首先，可以把它理解成一个函数的内部状态的遍历器，每调用一次，函数的内部状态发生一次改变（可以理解成发生某些事件），ES6引入Generator函数，左右就是可以完全控制函数的内部状态的变化，依次遍历这些状态。
在形式上，Generator是一个普通函数，但是有两个特征：
1. function 命令与函数名之间有一个星号 * 
2. 函数体内使用 yield 语句，定义遍历器的每个成员，即不同的内部状态（yield语句在英语里的意思就是产出）

## Promise 对象
### 基本用法
ES6原生提供了Promise对象，所谓 Promise 对象，就是代表了未来某个将要发生的事件（通常是一个异步操作）。它的好处在于，有了promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise对象还提供了一整套完整的接口，使得可以更加容易的控制异步操作。
ES6的Promise对象是一个构造函数，，用来生成Promise实例。

``` javascript
function test() {
  return new Promise((resolve, reject) => {
    var num = Math.random()
    if (num > 0.5) {
      resolve(num + '大于0.5')
    } else {
      reject(num + '小于0.5')
    }
  })
}
test().then((res) => {
  console.log(res)
}).catch((error) => {
  console.log(error)
})
```

### Promise.prototype.then 链式操作
### Promise.prototype.catch 捕获错误
### Promise.all 方法
该方法用于将多个promise实例，包装成一个新的promise实例，可用于多个异步操作同时满足某个条件后进行操作。
只有p1,p2的状态都变成了 fulfilled，p的状态才会fulfilled,然后执行then里的方法
当p1,p2中有一个被rejected，p的状态就变成了，rejected，然后执行catch里的方法

``` javascript
function test(id) {
  var ppp =  new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log(id)
      if (id > 0) {
        resolve()
      } else {
        reject()
      }
    }, 2000)
  })
  return ppp
}
var promiseAll = [1,2].map((id) => {
  return test(id)
})
Promise.all(promiseAll).then(() => {
  console.log('ok')
}).catch(() => {
  console.log('no')
})
```

### Promise.race 方法
同 Promise.all 类似，但是只要p1,p2有一个实例先改变了状态，p的状态就跟着改变，那个率先改变的实例，就是返回值
### Promise.resolve方法 Promise.reject方法
### async 函数
async 函数是用来取代回调函数的另一种方法。
只要函数名之前加上async关键字，就表明该函数内部有异步操作。该异步操作应该返回一个promise对象。前面用await关键字注明。当函数执行的时候，一旦遇到await就会先返回，等到触发的异步操作完成，再接着执行函数提内后面的语句
async 函数并不属于ES6,而是被列入ES7内。但是部分浏览器已实现了该功能。

``` javascript
async function asyncValue() {
  var a = 0
  await new Promise((resolve) => {
    setTimeout(() => {
      a++
      resolve()
    }, 3000)
  })
  return a;
}

asyncValue().then((res) => {
  console.log(res)
}).catch((error) => {
  console.log(error)
})
```

## Class 和 Module
### Class
ES5通过构造函数，定义并生成新对象。

``` javascript
function Point(x, y) {
  this.x = x
  this.y = y
}
Point.prototype.toString = function() {
  return '(' + this.x + ', ' + this.y + ')'
}
Point.prototype.mj = function() {
  return this.x * this.y
}
Point.prototype.bc = function() {
  return (this.x + this.y ) * 2
}

var p = new Point(4,6)
console.log(p.mj())
console.log(p.bc())
```
ES6引入了Class这个概念，作为对象的模版，通过class关键字，可以定义类，上面的代码用‘类’改写，就是下面这样：

``` javascript
class Point {
  constructor (x, y) {
    this.x = x
    this.y = y
  }
  toString () {
    return '(' + this.x + ', ' + this.y + ')'
  }
}
var po = new Point(2,4)
po.toString() // (2, 4)
```
class 之间可以使用 extends 关键字，实现继承。

``` javascript
class ColorPoint extends Point {}
```
上面代码定义了一个ColorPoint类，该类通过关键字 extends ，继承了Point类所有的属性和方法。但是由于没有部署任何代码，所以这两个类完全一样，等于复制了一个Point类。下面，我们在ColorPoint内部加上代码。

``` javascript
class ColorPoint extends Point {
  constructor (x, y, color) {
    super(x, y)
    this.color = color
  }
  toString () {
    return this.color + ' ' + super()
  }
}
```

上面代码中，constructor方法和toString方法中，都出现了super关键字，它代指弗雷的同名方法，在constructor方法内，super指代父类的constructor方法；在toString方法内，super指代父类的toString方法。
有一个地方需要注意，类和模块的内部，默认就是严格模式，所以不需要使用use strict 置顶运行模式，考虑到未来所有的代码，其实都是运行在模块之中的，所以ES6实际上把整个语言升级到了严格模式。

### Module 的基本用法
javascript没有模块(module)体系，无法讲一个大城县拆分成互相依赖的小文件，再用简单的方法拼装起来，其他语言都有这项功能，比如ruby的require，python的import 甚至css都有 @import,但是javascript任何这方面的支持都没有，这对开发大型的、复杂的项目形成了巨大障碍。
在ES6之前，社区制订了一些模块加载的方案，最主要的有commonJs和AMD两种，前者用于服务器，后者用于浏览器，成为浏览器和服务器通用的模块解决方法。
ES6模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量，CommonJS和AMD模块，都只能在运行时确定这些东西，比如，CommonJSmok 模块就是对象，输入时必须查找对象属性。

``` javascript
var {stat, existx, readFile} = require('fs')
```
ES6模块不是对象，而是通过 export命令显式置顶输出的代码，输入时也采用静态命令的形式
``` javascript
import (stat, exists, readFile) from 'fs'
```
#### export 命令，import 命令
模块功能主要由两个命令构成：export和import。export命令用于用户自定义模块，规定对外接口；import命令用于输入其他模块提供的功能。同事创造命名空间（namespace），防止函数名冲突。
ES6允许将独立的JS文件作为模块，也就是说，允许一个javascript脚本文件调用另一个脚本文件，该文件内部的所有变量，外部无法获取，必须使用export关键字输入变量。下面是一个JS文件，里面使用export关键字输出变量。

``` javascript
// config.js
const host = 'qq.com'
const ip = '1.1.1.1'
const getInfo = function(){
  return 'something'
}
module.export = {
  host,
  ip,
  getInfo
}

// app.js
const { host, getInfo } = require('./config')
console.log(host)  // qq.com
console.log(getInfo())  // something
```
#### 模块的整体输入，module命令
#### export default 命令

### 模块的继承
模块之间也可以继承。