---
title: 'React Fiber'
date: 2019-06-08T11:31:09+08:00
draft: true
---

react16 的大改动是重构了

react 15: stack reconciler

react 16: fiber reconciler

diff 算法，原来一口气要做完所有更新操作，现在可以利用 16ms 的

## 原因

扩大适用性，动画，布局和手势。

jsx，天然的嵌套结构，递归，简单好理解。
缺点，不可中断。如果做动画等 js 长时间执行的情况，就会出现 卡顿，丢帧的情况
