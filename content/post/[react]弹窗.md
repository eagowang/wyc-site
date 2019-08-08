---
title: "[React]弹窗"
author: "eago"
tags: ["react", "弹窗", "高阶组件"]
categories: ["react"]
date: 2019-08-01T20:56:06+08:00
draft: false
---

如何实现一个通用的弹窗组件？

<!--more-->

日常工作中，很多地方都会用到弹窗，确认框，弹出操作框，错误提示等。在每个组件中都维护一个状态：visible，两个事件：setVisible 为 true 或 false。很麻烦。

用过 antd 都知道 antd 中 message 和 notification 这两个组件可以直接打开弹窗并关闭，即 `message.error('失败')`

## 总体思路

实现的思路就是实现一个高阶组件，接收 Message 或 Notification 这样的组件，在 show 方法中显示并返回组件实例，在 hide 方法中隐藏

## 完整的代码：

<iframe src="https://codesandbox.io/embed/danchuang-lhy50?fontsize=14" title="弹窗" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

## 关键代码解释

1. show 方法中调用`ReactDOM.render()`目的是将“弹窗组件”渲染到一个 div 载体（overlap）上，并拿到弹窗组件的实例
2. render 方法拿到 show 方法中调用的 props 和 children，clone children 并添加 close 方法。再使用`ReactDOM.createPortal()`真正的添加到 dom 中。
3. close 方法使用 unmountComponentAtNode 卸载掉载体（overlap）
