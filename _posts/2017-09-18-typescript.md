---
layout: post
category: "javascript"
title: "TypeScript 笔记总结"
tags: ["typescript", "es6"]
---

## 简介
### 什么是TypeScript?
首先官网的定义是

```
TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. Any browser. Any host. Any OS. Open source.
```
意思是 typescript 是javascript的一个超集，它可以编译成javascript，编译出来的javascript可以在任何浏览器上运行，它的编译工具可以运行在任何系统和服务器上，它是开源的。

为何选择TS？

- ts增加了代码的可读性和可维护性。
    - 拥有类型系统
    - 可以在编译阶段发现大部分错误
    - 增强了IDE和编辑器的功能，包含代码补全，接口提示等。
- typescript 非常的包容
    - ts 是javascript的超集，.js文件可以直接命名为.tx即可。
    - 即使不显示的定义类型，也能自动做出类型推论
    - 可以定义从简单到复杂的一切类型
    - 即使ts编译器报错，也可以生成js文件
    - 兼容第三方库，及时第三方库不是ts写的，也可以编写单独的类型文件提供ts读取。
- ts拥有活跃的社区支持
    - 大部分第三方库都有提供给ts的类型定义文件
    - google开发的angular就是使用ts编写的
    - es6的一部分特性是借鉴的ts的
    - ts拥抱es6的规范,也支持部分es7草案的规范
- typescript的缺点
    - 有一定的学习成本，需要理解一些前端工程师可能不熟悉的概念，而且中文资料可能也不多
        - 接口 interfaces
        - 泛型 Generics
        - 类 Classes
        - 枚举类型 Mnums
    - 短期内可能会增加一些开发成本，毕竟要多写一些类型的定义，不过对于一个需要长期维护的项目，ts能够减少其维护成本
    - 集成到构建流程需要一些工作量
    - 可能和一些库结合的不是很完美

### 安装typescript
typescript 命令工具的安装方法如下：

``` bash
# 安装
npm install -g typescript
# 使用
tsc app.ts
```

### Hello TypeScript
ts中使用***：***为变量指定类型，前后有无空格都可以。
``` ts
function sayHello(person: string) {
    return 'hi, ' + person
}
let user = ['quinn', 'mk']
console.log(sayHello(user))
// 这里编译后会报错，person应该为字符串类型，但是传进去的是数组，但是仍然会生成.js文件
```
## 基础
### 原始数据类型
javascript的类型分为两种：原始数据类型和对象类型
- 原始数据类型
##### 布尔值
布尔值是最基础的数据类型，在TS中使用，boolean 定义布尔值的类型
``` ts
let idDone: boolean = false
```
#### 数值
使用number定义数值类型：
``` ts
let count: number = 10
let hexCount: number = 0xaf
let binaryCount: number = 0b1001010
let eightCount: number = 0o1743
let notNumber: number = NaN
let infinityNumber: number = Infinity
```
#### 字符串
使用string定义字符串类型：
``` ts
let myName: string = 'quinn'
let myAge: number = 22
let sentence: string = `hello, my name is ${myName}, I will be ${myAge+1} years old next month.
```
#### 空值
javascript没有空值（void）的概念，在TS中，可以使用`void`表示没有任何返回值的函数：
``` ts
function alertName(): void {
    alert('hi')
}
```
声明一个`void`类型的变量没有什么用，因为你只能将它赋值为`undefined`和`null`
``` ts
let un: void = undefined
```
#### null 和 undefined
在ts中，可以使用`null`和`undefined`来定义这两个原始数据的类型
```
let n: null = null
let u: undefined = undefined
```
`undefined`类型的变量只能被赋值为`undefined`，`null`类型的变量只能被赋值为`null`
与`void`的区别是，`undefined`和`null`是所有类型的子类型，也就是说`undefined`类型的变量，可以赋值给`number`类型的变量：
```
let num: number = undefined
//  这样不会报错
```
而`void`类型的变量不能赋值给number类型的变量：
```
let u: void;
let num: number = u
// 这里就会报错
```

### 任意值
任意值（any）用来表示允许赋值为任意值类型。
#### 什么是任意值类型
如果一个普通类型，在赋值过程中改变类型是不被允许的：
```
let myName: string = 'seven'
myName = 7
// 这会报错
```
但是如果是`any`类型，则允许被赋值为任意类型的。
#### 任意值的属性和方法
在任意值上访问任何属性都是允许的：
```
let anyThing: any = 'hello'
console.log(anyThing.myName)
console.log(anyThing.myName.firstName)
```
也允许调用任何方法
```
let anything: any = 'haha'
anything.setName('quinn')
anything.setName('qu').sayHello()
anything.myname.setFirstName('cat')
```
可以认为，声明一个变量为任意值之后，对它的任何操作，返回的内容的类型都是任意值。
#### 未声明类型的变量
变量如果在声明的时候，未致命其类型，那么它会被识别为任意值类型：
```
let something;
something = 'some'
something = 7;

something.setName('jerry lee');
```
等价于
```
let something:any;
something = 'some'
something = 7
something.setName('jerry lee')
```
### 类型推论
如果没有明确的指定类型，那么ts会依照类型推论的规则推断出一个类型。
#### 什么是类型推论
以下代码虽然没有指定类型，但是会在编译的时候报错:
```
let myNum = 'seven'
myNum = 7
// 这里会报错
```
事实上，它等价于：
```
let myNum: string = 'seven'
myNum = 7
```
ts 会在没有明确的指定类型的时候推测出一个类型，这就是类型推论。
***在ts2.1之前，如果定义的时候没有赋值，不管之后有没有赋值，都会被推断成`any`类型而完全不被类型检查：***
```
let myNum;
myNum = 'seven'
myNum = 7
```
ts 2.1中，编译器会考虑对myNum的最后一一次赋值来检查类型。
### 联合类型
联合类型表示取值可以为多种类型中的一种。
#### 简单的例子
```
let myNum: string | number
myNum = 'seven'
myNum = 7
```
```
let myNum: string | number
myNum = true
// 报错
```
联合类型使用`|`分隔每个类型。
这里的`string|number`的含义是，允许`myNum`的类型是`string`或者`number`，但不能是其他的类型。
#### 访问联合类型的属性或方法
当ts不确定一个联合类型的变量到底是哪个类型的时候，我们***只能访问此联合类型的所有类型里公有的属性或方法：***
```
function getLength(something: string|number) {
return something.length
}
```
上例中`length`不是`string`和`number`的公有属性，所以会报错。
访问`string`和`number`的公有属性是没有问题的：
```
function getString(something: string|number) {
    return something.toString()
}
```
联合类型的变量在被赋值的时候，会根据类型推论的规则推断出一个类型
```
let myNum: string|number
myNum = 'seven'
console.log(myNum.length)
myNum = 7
console.log(myNum.length)
// 报错
```
上例中，第二行，`myNum`被推断成了`string`，访问他的`length`属性不会报错。
而第四行的`myNum`被推断成了`number`，访问他的`length`属性就会报错。
### 对象的类型---接口
在ts中，我们使用接口（interfaces）来定义对象的类型。
#### 什么是接口
在面向对象语言中，接口（interfaces）是一个很重要的概念，它是对行为的抽象，而具体如何行动需要由类（classes）去实现（implements）
ts中的接口是一个非常灵活的概念，除了可用于 对类的一部分行为进行抽象 以外，也常用于对【对象的形状】进行描述。
#### 简单的例子
```
interface Hero {
name: string;
id: number
}
let q = {
name: 'quinn',
id: 1
}
```
上面的例子中，我们定义了一个接口`Hero`,接着定了一个变量`q`,他的类型是`Hero`。这样，我们就约束了`q`的形状必须和接口`Hero`一致。
接口一般首字母大写。
定义的变量比接口少了一些属性是不允许的：
```
interface Hero {
name: string;
id: number
}
let q: Hero = {
name: 'xiaoming'
}
// 这里就会报错的
```
多一些属性也是会报错的
```
interface Hero {
name: string;
id: number
}
let q: Hero = {
name: 'quinn',
id: 44,
weapon: 'gun'
}
// 也会报错的
```
可见，***赋值的时候，变量的行装必须和接口的形状保持一致。***
#### 可选属性
有时候我们希望不要完全匹配一个形状，那么可以用可选属性：
```
interface Hero {
name: string;
id: number;
age?:number
}

let q: Hero = {
name: 'quinn',
id: 1
}
// 不会报错，是正确的，可选属性可以不添加。
```
可选属性的含义是该属性可以不存在。
但是这时***仍然不允许添加未定义的属性***
#### 任意属性
有时候我们希望一个接口允许有任意的属性，可以使用如下方式：
```
interface Hero {
name: string;
id: number;
age?: number;
[propName: string]: any;
}
let q: Hero = {
 name: 'quinn',
 id: 7,
 weapon: 'gun'
}
```
使用`[propName: string`定义
需要注意的是，***一旦定义了任意属性，那么确定属性和可选属性都必须是它的自属性***
```
interface Hero {
name: string;
age?: number;
[propName: string]: string
}

let q: Hero = {
name: 'quinn',
age: 22,
weapon: 'gun'
}
```
上例中，任意属性的值允许是 string,但是可选属性 age 的值却是 number,number不是string的子属性，所有报错。
#### 只读属性
有时候我们希望对象中的一些字段只能在创建的时候被赋值，那么可以用 readonly 定义只读属性：
```
interface Hero {
readonly id: number,
name: string,
age?: number,
[propName: string]: any;
}
let q: Hero = {
id: 1,
name: 'quinn',
age: 22,
weapon: 'gun'
}
q.id = 888
// 这里修改id属性的值就会报错
```
只读属性的约束存在于第一次给对象赋值的时候，而不是第一次给只读属性赋值的时候：
```
interface Hero {
readonly id: number;
name: string
}
let q: Hero = {
name: 'quinn'
}
q.id = 78
// 这里会出现两个错误，第一个是，没有给id赋值，第二个是id不能修改
```
### 数组的类型
在ts中，数组类型有多种定义方式，比较灵活。
#### [类型+方括号]表示法
最简单的方法是使用[类型+方括号]表示法：
```
let arr: number[] = [1,2,3]
```
数组中的项目不允许出现其他的类型：
```
let arr: number[] = [1,'2',3]
// 会报错，数组元素只能是 number

let arr: number[] = [1,2]
arr.push('3')
// 这里也会报错，新增的数据类型只能是number
```
#### 数组泛型
也可以使用数组泛型，Array<elemType> 来表示数组：
```
let arr: Array<number> = [1,2,3]
```
#### 用接口表示法
接口也可以用来描述数组：
```
interface NumberArray {
[index: number]: number
}
```
NumberArray 表示：只要index的类型是number,那么值的类型必须是number.
#### any 在数组中的应用
一个比较常见的做法是，用any表示数组中允许出现任意类型：
```
let arr: any[] = [1,'seven',{name: 'quinn'}, true,null,undefined]
```
#### 类数组
类数组不是数组类型，比如arguments:
```
function sum() {
let args: number[] = arguments;
}
// 会报错，这里它有自己的接口定义，如 IArguments, NodeList, HTMLCollection 等
function count() {
let args: IArguments = arguments;
}
```
### 函数的类型
#### 函数声明
在js中，有两种常见的定义函数的方式，---函数声明和函数表达式
```
// 函数声明
function sum(x, y) {
return x+y;
}

// 函数表达式
let mySum = function (x, y) {
return x + y;
}
```
一个函数有输入和输出，要在ts中对其进行约束，需要把输入和输出都考虑到，其中函数声明的类型定义较简单：
```
function sum(x: number, y: number): number {
return x+y
}
```
注意，***输入多余的（或者少于要求的）参数，是不被允许的：
```
function sum (x: number, y: number): number {
return x+y
}
sum(1,2,3)
//会报错
sum(1)
//也会报错
```
#### 函数表达式
如果要我们现在写一个函数表达式的定义，可能会写成这样：
```
let mySum = function(x: number, y: number): number {
return x + y;
}
```
这是可以通过编译的，不过事实上，上面的代码只对等号右侧的匿名函数进行了类型定义，而等号左边的mySum，是通过赋值操作进行类型推到而推断出来的。如果需要我们手动给mySum添加类型，则应该是这样的：
```
let mySum: (x:number, y: number) => number = function (x: number, y: number): number {
return x + y
}
```
#### 可选参数
与接口中的可选属性类似，我们用`?`表示可选参数：
```
function buildName(firstName: string, lastName?: string ){
return lastName ? firstName + lastName : firstName;
}
```
需要注意的是：可选参数必须接在必选参数后面。换句话说，可选参数后面不允许再出现必须参数了。
#### 默认参数
在ES6中，我们允许给函数的参数添加默认值，ts将会添加了默认值的参数识别为可选参数：
```
function sum (x: number, y: number = 5) {
return x + y
}
```
let a = sum(1,2)
let b = sum(4)
此时就不受【可选参数必须接在必选参数后面】的限制了
#### 剩余参数
ES6中，可以使用`...rest`的方式获取函数中的剩余参数（rest参数）
```
function push(array, ...items: any[]) {
items.forEach((item) => {
array.push(item)
})
}
let a = []
push(a,1,2,3,4)
```
注意 ...rest参数只能是最后一个参数，关于rest参数，可以参考ES6中的rest参数
#### 重载
重载允许一个函数接受不同数量或者类型的参数时，做出不同的处理。
比如，我们需要实现一个函数`reverse`，输入数字123的时候，输出反转的数字321，输入字符串`hello`的时候，输出反转的字符串`olleh`。
那么利用联合类型，我们可以这么实现：
```
function reverse(x: number | string): number | string {
    if (typeof x === 'number') {
        return Number(x.toString().split('').reverse().join(''))
    }
    else if (typeof x === 'string') {
        return x.split('').reverse().join('')
    }
}
```
然而这样有一个缺点，就是不能够精确的表达，输入为数字的时候，输出也应为数字，输入为字符串的时候，输出也应为字符串。
这时，我们可以使用重载定义多个`reverse`的函数类型：
```
function reverse(x: number): number;
function reverse(x: string): string;
function reverse(x: number|string): number | string {
if (typeof x === 'number') {
    return ...
}
else if (typeof x === 'string') {
    return ...
}
}
```
上例中，重复定义了多次函数`reverse`，前几次都是函数定义，最后一次是函数实现。在编辑器的代码提示中，可以正确的看到前两个提示。
注意，ts会优先从最前面的函数定义开始匹配，所有多个函数定义如果由包含关系，需要优先把精确的定义写在前面。
### 类型的断言
类型断言可以用来绕过编译器的类型推断，手动指定一个值的类型（即程序员对编译器断言）
#### 语法
```
<类型>值
// 或
值 as 类型
// 在TSX语法（react的JSX语法的TS版）中必须使用后一种
```
### 声明文件
当使用第三方库时，我们需要引用它的声明文件。
#### 声明语句
加入我们想使用第三方库，比如jQuery，我们通常这样获取一个id是foo的元素
```
$('#foo')
// or
jQuery('#foo')
```
但是ts中，我们并不知道$或者jQuery是什么东西。
这时候，我们需要使用 declare 关键字来定义它的类型，帮助ts判断我们传入的参数类型对不对。
```
declare var jQuery: (string) => any;
jQuery('#foo')
```
#### 声明文件
通常我们会把类型声明放到一个单独的文件中，这就是声明文件：
```
// jQuery.d.tx
declare var jQuery: (string) => any;
```
我们约定声明文件以`.d.ts`为后缀。
然后在使用到的文件的开头，用[三斜线]表示引用了声明文件：
```
/// <reference path="./jQuery.d.ts" />
jQuery('#foo')
```
### 内置对象
js中有很多内置对象，他们可以直接在ts中当作定义好了的类型。
内置对象是指根据标准在全局作用域上存在的对象。这里的标准是指的ES和其他环境（比如DOM）的标准
#### ECMAScript 的内置对象
ECMAScript 标准提供的内置对象有：
Boolean, Error, Date, RegExp等。
我们可以在ts中将变量定义为这些类型：
```
let b: Boolean = new Boolean(1);
let e: Error = new Error('Error')
let d: Date = new Date()
let r: RegExp = /\d/
```
#### DOM和BOM的内置对象
DOM和BOM提供的内置对象有：
Document, HTMLElement,Event,NodeList等。
ts中会经常用到这些类型：
```
let body: HTMLElement = document.body
let allDiv: NodeList = document.querySelectorAll('div')
document.addEventListener('click',function(e: Event) {
// do something...
}
)
```
#### ts核心库的定义文件
ts核心库的定义文件中定义了所有浏览器环境需要用到的类型，并且是预设在ts中的。
当你在使用一些常用的方式的时候，ts实际上已经帮你做了很多类型判断的工作了，比如：
Math.pow(10,'2')
上面的例子中，Math.pow必须接受两个
#### 用ts写nodejs
Node.js不是内置对象的一部分，如果想用ts写nodejs,则需要引入第三方声明文件：
```
npm install @types/node --save-dev
```

## 进阶
### 类型别名
### 字符串字面量类型
### 元组
### 枚举
### 类
### 类与接口
### 泛型
### 声明合并
### 扩展阅读