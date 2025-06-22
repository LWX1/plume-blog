---
title: qiankun
createTime:  2023-02-01
isShowComments: false
tags:
    - qiankun
categories:
    - qiankun
---

## 起源

- qiankun是阿里开源的一个微前端的框架
- 基于single-spa封装的，提供了更加开箱即用的API
- 技术栈无关，任意技术栈的应用均可使用/接入，不论是 React/Vue/Angular/jQuery 还是其他等框架。
- HTMLEntry的方式接入，像使用iframe一样简单
- 实现了single-spa不具备的样式隔离和js隔离
- 资源预加载，在浏览器空闲时间预加载未打开的微应用资源，加速微应用打开速度。

## 核心概念

- 主应用（基座）：整个微前端的入口，负责加载和管理子应用。
- 子应用：独立的前端项目，可以独立开发，独立部署，独立运行。
- 生命周期：主应用和子应用之间的生命周期钩子，控制应用的加载、启动和卸载。
- 沙箱：隔离子应用的运行环境，防止冲突和污染。
