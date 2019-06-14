---
title: "[学习]microtask,macrotask"
date: 2019-06-14T21:28:59+08:00
draft: false
keywords: ['学习系列']
description: '作用域、闭包、原型链'
tags: ['学习系列', 'microtask', 'macrotask']
categories: ['学习系列']
author: 'eago'
comment: true
---
[Tasks, microtasks, queues and schedules](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)

用一句话概括，就是一个macrotask中出现的mircotask都在这一次eventloop中执行，出现的macrotask需要在新的eventloop执行


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
console.log('script start');
setTimeout(function(){
    console.log('setTimeout');
}, 0);

Promise.resolve().then(function(){
    console.log('promise1');
}).then(function(){
    console.log('promise2')
})

console.log('script end')
```

```
script start
script end
promise1
promise2
setTimeout
```

1. 一次event loop
2. setTimeout的回调进入macrotask栈
3. 带promise1的回调进入microtask栈
4. 执行3的回调，并出栈
5. 带promise2的回调进入microtask栈
6. 执行5的回调，并出栈
7. 没有microtask任务了
8. 新一次event loop
9. 执行2的macrotask

