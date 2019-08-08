---
title: "microtask,macrotask"
author: "eago"
tags: ["microtask,macrotask"]
categories: ["js"]
date: 2019-06-14T21:28:59+08:00
draft: false
---

[Tasks, microtasks, queues and schedules](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)

用一句话概括，就是一个 macrotask 中出现的 mircotask 都在这一次 eventloop 中执行，出现的 macrotask 需要在新的 eventloop 执行

## macrotask(task)

- setTimeout
  = setInterval
- setImmediate
- requestAnimationFrame
- I/O
- UI rendering

## microtask

- process.nextTick
- promise callback

例子：

```js
console.log("script start");
setTimeout(function() {
  console.log("setTimeout");
}, 0);

Promise.resolve()
  .then(function() {
    console.log("promise1");
  })
  .then(function() {
    console.log("promise2");
  });

console.log("script end");
```

```
script start
script end
promise1
promise2
setTimeout
```

1. 一次 event loop
2. setTimeout 的回调进入 macrotask 栈
3. 带 promise1 的回调进入 microtask 栈
4. 执行 3 的回调
5. 带 promise2 的回调进入 microtask 栈
6. 执行 5 的回调
7. primise2 出栈
8. promise1 出栈
9. 没有 microtask 任务了
10. 新一次 event loop
11. 执行 2 的 macrotask
