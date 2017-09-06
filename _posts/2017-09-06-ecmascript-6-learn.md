---
layout: post
category: "javascript"
title: "EcmaScript 6 学习笔记"
tags: ["es6", "ecmascript"]
---

# EcmaScript 学习指南
学习 [EcmaScript 6 入门](https://wohugb.gitbooks.io/ecmascript-6/content/)


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
```javascript
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
```javascript
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
```javascript
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