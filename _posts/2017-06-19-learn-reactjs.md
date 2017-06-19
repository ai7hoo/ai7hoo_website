---
layout: post
category: "javascript"
title: "React.js 入门学习笔记"
tags: ["Reactjs"]
---

### React.js 知识点总结：
之前已大量使用过 Vue.js 所以对于学习 React.js 有所帮助，看起来还是 Vue.js 好学一些。
测试在浏览器环境使用，文件引入：

```
-- react.js		核心文件
-- react-dom.js	DOM操作相关
-- babel.js		JSX 转换成 js, 只是在测试的时候使用，实际生产环境需要在服务器端转换完成再使用
```

### JSX 文件
jsx 文件可以写在 script 里面，但是要注意 type = text/babel, 不可以直接作为 javascript 使用。

### 组件
#### 创建组件
``` jsx

var MyCom = React.createClass({
	// 设置 props 默认值
	getDefaultProps() {
		return {
			title: 'Default Title'
		}
	},
	// 设置 state 默认值
	getInitialState() {
		return {
			count: 5,
			maxNum: 10
		}
	},
	// btn 事件
	addCount() {
		if(this.state.count >= this.state.maxNum){
			return false
		}
		this.setState({
			count: this.state.count+1
		})
	},
	// 渲染结构
	render() {
		return (
			<div ref="rootbox">
				<h3>{this.props.title}</h3>
				<div>{this.count}</div>
				<button onClick="addCount">click</button>
			</div>
		)
	}
})
```

#### 使用组件

``` jsx
ReactDOM.render(
	<MyCom title="this is a title" />,
	document.getElementById('app')
)
```