---
title: 'React协调'
date: 2019-06-08T11:31:09+08:00
draft: true
---

react 15: stack reconciler

react 16: fiber reconciler

## 原因

jsx，天然的嵌套结构，递归，简单好理解。
缺点，不可中断。如果做动画等 js 长时间执行的情况，就会出现 卡顿，丢帧的情况
