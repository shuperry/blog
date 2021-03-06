---
title: 深入理解 Vue2.0 概念
date: 2020-08-06 14:30:00
updated:
tags:
  - vue
  - mvvm
categories: 前端
comments: true # 开启回复功能
toc: false # 开启自动生成目录
---
　　很多人经常在项目中使用 Vue，但是只停留在使用，没有深究其深层次的原理，理解 Vue 有助于我们写出质量更好的程序，深层次理解 JS 底层技术的应用，为使用新技术打好基础。
<!--more-->

### Vue 的核心理念

---

#### 为什么会有 Vue

首先我们来梳理以前的项目里的做法：
  1、在 html 中引入 js 和 css
  2、在 html 的 script 标签中写 js
  3、在前端写 java 代码
  4、同样的功能如果在其它地方还有用到，只怕只是个很小的改动，都需要再重写一遍
  5、使用 jQuery 等工具直接操作 dom

如果只是小项目，我们这么做完全可以接受，但是一旦项目达到一定规模，项目维护起来将是个灾难。

于是出现了 `Angular`、`React`，再然后出现了 `Vue`，关于这三个框架的比较，我们以后再继续说，这里只说 `Vue`。

Vue 的核心库只关心视图层，易于上手，也能够为复杂的单页面应用提供驱动。

#### Vue 有什么特点

##### 轻量级

Vue 组件会自动追踪组件实例中的自定义和计算属性，API 简单、灵活，页面中渲染数据使用类 Mustache 语法，读者很容易理解，可以很快上手。

##### 双向数据绑定

　　这个概念的官方叫法是响应式渲染，是官方核心概念之一，在组件的 data 函数中声明属性，在可输入元素中使用 v-model 指令绑定该属性，在页面内容有变化时，在组件中其它位置如果也有用到这个属性，会自动更新，同样，在组件内有业务操作修改了这个属性，在页面上也可以马上看到变化，并且响应极快。

##### 组件化

这是 Vue 核心概念之一，组件化的好处是提升代码的复用性，包括组件内部的业务逻辑代码、页面元素及样式，可以通过 `props` 参数实现组件在不同业务调用时的差异化，根据业务需要封装自定义组件，组件化不仅可以提升代码复用性，同样可以优化项目文件结构，在一个组件中只做一件事，单位业务逻辑代码量会减少很多，提升代码可读性和可维护性。

父组件向子组件传输数据可以使用 `props` ，子组件与父组件通信时，通过 `emit` 触发父组件的事件，来通知父组件改变数据。

##### 指令

Vue 实现与页面交互，主要就是通过内置指令来实现，像 `v-for`、`v-if`、`v-bind`、`v-on` 等指令，很容易理解其用法。

同样我们也根据业务需要可以定制自己的指令，只需要在 Vue 实例中注册即可，一处定义，整个项目内部都可以使用。

##### 路由

路由 `vue-router` 其实不在 Vue 的核心代码中，是作为插件的方式由官方开发的，与 Vue 深度集成，用于管理 url 路径与组件间的映射关系。

##### 状态管理

我们知道 `React` 初开始流行的一大原因就是 `单向数据流`，为前端项目规范化提供了一个很好的概念，极大的提升了项目的维护便利性。

`单向数据流` 的意思是将业务数据按模块整合到一起取名叫 `store`，每个模块存放数据的区域叫 `state`，页面上的每一个业务操作都发起一个动作 `action`，在 action 内部向后台发起请求，根据请求返回的数据来根据需要提交修改 `mutation`，则 mutation 来修改当前模块 `state` 中的数据，每个操作都遵循这个规范，再加上日志打印，在数据出现错误时很方便可以追踪到导致数据错误的操作，由此来定位业务逻辑错误，增加了很多便利性和逻辑可控性。

在 `Vue` 中同样也有状态管理，简单的模块内同步数据与页面效果使用成本更低 `双向数据绑定` 功能即可实现，但有更复杂的业务逻辑和很多组件共用数据时，更推荐的用法是官方的插件 `vuex`，该插件提供了与上述 React 一样的单向数据流管理逻辑。
