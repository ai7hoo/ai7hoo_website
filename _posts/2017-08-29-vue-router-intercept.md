---
layout: post
category: "javascript"
title: "vue 路由拦截"
tags: ["vue", "前端路由"]
---

之前有一个项目使用 vue-cli 构建工具，在进行用户登录状态拦截的时候，使用了 vue 的路由过滤方式进行拦截。

``` javascript
// router/index.js
import Router from 'vue-router'
// 定义路由规则
const router = new Router({
  routes: [
    {
      path: '/login',
      component: (resolve) => {
        require(['pages/login'], resolve)
      }
    }, {
      path: '/userinfo',
      requireAuth: true,	// 该页面是否需要登录显示，用于拦截路由的字段
      component: (resolve) => {
        require(['pages/userinfo'], resolve)
      }
    }
  ]
})

// 使用路由的 beforeEach 钩子拦截非登录状态下的路由规则
router.beforeEach((to, from, next) => {
  // 通过判断每个规则的 requireAuth 字段是否为 true，并且本地是否存储了登录状态
  // 如果 requireAuth==true&&本地没有存储登录信息，则把路由跳转到登录页面
  if (to.requireAuth && !(window.localStorage.getItem('loginState'))) {
    next({
      path: '/login',
      query: to.fullPath
    })
  } else {
    next()
  }
})

export default router
```