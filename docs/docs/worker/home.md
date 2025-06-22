---
title: worker
createTime:  2024-3-3
isShowComments: false 
tags:
  - worker
categories:
  - worker
---

## 什么是worker

- Web Worker 是 HTML5 标准的一部分，是在主线程上开辟新的线程，但该线程不会影响主线程的运行。

- 因为存在两个独立的线程，worker 只需把大运算数据运行完后返回结果给js线程，这样页面就不会出现卡顿现象

## Web Worker 能干些什么

- worker 是单独开启的新线程，主要用于计算，所以不存在操作dom的document和window，但是会存在location和navigator对象可以以可读方式访问

- worker 中存在顶级对象self，主要通过self来与js线程进行通讯

