---
title: worker使用
createTime:  2024-3-3
isShowComments: false 
tags:
  - worker
categories:
  - worker
---



## Web Worker 使用

- 创建 worker 只需要通过 new 调用 Worker() 构造函数即可

```ts
const worker = new Worker(path, options);
```

> [!TIP]
> path路径为有效的js脚本的地址，必须遵守同源策略。无效的js地址或者违反同源策略，会抛出SECURITY_ERR 类型错误


## 线程通讯

```ts
// main.js（主线程/js线程）
const myWorker = new Worker('/worker.js'); 

// 接收消息
myWorker.addEventListener('message', e => { 
    console.log(e.data); 
});

// 向 worker 线程发送消息，对应 worker 线程中的 e.data
myWorker.postMessage('Greeting from Main.js'); 


// worker.js（worker线程）
// 接收到消息
self.addEventListener('message', e => { 
    console.log(e.data); // Greeting from Main.js，主线程发送的消息
    self.postMessage('Greeting from Worker.js'); // 向主线程发送消息
});

```

## 监听错误信息

```ts
// main.js（主线程）
const myWorker = new Worker('/worker.js'); // 创建worker

myWorker.addEventListener('error', err => {
    console.log(err.message);
});
myWorker.addEventListener('messageerror', err => {
    console.log(err.message)
});

```
