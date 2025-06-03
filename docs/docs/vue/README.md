---
title: vue
createTime:  2020-11-01
isShowComments: false
tags:
    - vue
categories:
    - vue
---

## vue 是什么

-   vue 是一个用于构建前端页面的一个渐进式 Javascript 框架的单页面应用；相对比以前的传统前端通过 DOM 直接操作页面开发，vue 通过牺牲 js 来批量操作 DOM，让数据驱动视图的方式，让开发更加简单和方便。

## 渐进式

### 含义

-   没有多做职责之外的事，只做自己该做的事，不想做的，可以不做。就是<font color="orange">vue</font>不强求你一次性接受并使用它的全部特性。

## 单页面

### 原理

-   第一次进入请求一个 html 文件，加载组件需要的文件；当页面切换时，js 感知 url 变化，js 清除当前页面得内容，挂载新页面内容进来，所以页面切换特别快，首次加载时间长。

## Vue 核心特性

### 数据驱动（MVVM）

-   MVVM(Model-View-ViewModel)

1. Model：模型层，负责处理业务逻辑以及和服务器端进行交互

2. View：视图层，HMTL 页面的渲染

3. ViewModel：视图模型层，用于连接 Model 和 View，是两者的桥梁。

-   如下
    ![结果](/img/vue/mvvm.jpg)

## 组件化

### 什么是组件化

-   组件化，就是把页面拆分成多个组件，每个组件的 css、js、模板、图片等资源都放在一起维护；组件是资源独立的，组件在系统里可复用。

### 优势

-   降低系统耦合度；各个组件之间可以单独存在

-   维护方便；组件都写在一起。

-   提高开发效率；组件之间可以相互复用

## 指令

-   条件渲染指令 v-if

-   列表渲染指令 v-for

-   属性绑定指令 v-bind

-   事件绑定指令 v-on

-   双向数据绑定指令 v-model

-   文本指令,相当于 innerText v-text

-   hmlt 指令,相当于 innerHtml v-html

-   跳过编译指令，v-pre

-   保持在元素上直到关联实例结束时进行编译，在页面加载时有闪烁问题（插值闪烁问题）。v-cloak

-   只渲染一次，v-once
