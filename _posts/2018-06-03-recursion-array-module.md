---
layout: post
category: "javascript"
title: "模块依赖顺序加载原理分析"
tags: ["javascript"]
---

最近面试遇到一个题目，解释模块依赖加载的原理，思考下有以下几个步骤：
- 解析依赖
- 加载依赖
- 解析该模块
- 加载完成开始执行回调

回来后仔细思考其中当多个文件相互依赖的时候，如何处理依赖关系顺序，这个还没有具体去实现过。所有想理解下其中的原理。

开始可以先把该问题简化成以下一个问题：

``` javascript
// 有以下数组，每个元素有id和dep属性，其中dep属性是一个数组
// dep属性的子元素的数字代表着它所依赖的某个对象的id值
// 通过处理，实现输出顺序 1,2,3
// 其实就是没有依赖的放在最前面，然后后面的会依赖前面的
var arr = [
    {
        id: 3,
        dep: [1, 2]
    },
    {
        id: 1,
        dep: []
    },
    {
        id: 2,
        dep: [1]
    },
]

```
思路解析：
1. 先把没有依赖的放在最前面
2. 有依赖的就去循环每一个依赖id，并与之前的做对比，并使用递归的方式循环引用

实现方式：
``` javascript
// 就是一个根据依赖排序的问题
function sortById(list, result) {
  // 因为会使用到递归，而第一次可以不用传入，所以这里进行一次判断是否是第一次，如果是就赋一个空数组
  var result = result || []
  // 使用从后往前的方式进行循环，方便使用splice删除元素而不影响循环
  for (let i = list.length - 1; i >= 0; i--) {
    if (list[i].dep.length < 1 || !list[i].dep) {
      // 如果依赖长度为空，或者依赖没有写dep，则直接添加到结果result里，并使用splice在原数组list中删除
      result.unshift(list[i])
      list.splice(i, 1)
    } else {
      // 如果有依赖，首先定义一个计数器，该计数器等于依赖长度
      let count = list[i].dep.length
      // 循环每一个依赖的id
      for (let j = 0; j < list[i].dep.length; j++) {
        // 使用map遍历结果数组，判断结果中是否已经有该依赖了，如果有就为coutn减1
        result.map((v) => {
          if (v.id == list[i].dep[j]) {
            count = count - 1
          }
        })
      }
      // 判断结果count是否等于0了，如果是说明，该元素的依赖已经全部提取出来了，可以进行提取
      if (count <= 0) {
        result.push(list[i])
        list.splice(i, 1)
      }
    }
  }
  // 判断原数组的长度是否为0，如果没有就通过递归的方式，再次去引用自身
  if (list.length > 0) {
    sortById(list, result)
  }
  // 如果结束了就返回结果数组的id值
  return result.map((v, i) => v.id)
}

console.log(sortById(arr))
// 输出 [1,2,3]
```
以上只是处理依赖顺序的方式，具体的模块的加载要复杂很多，还要去创建标签，放到dom中，然后加载js文件等。