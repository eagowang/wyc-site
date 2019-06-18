---
title: '[学习]promise'
date: 2019-06-17T09:59:11+08:00
draft: true
keywords: ['学习系列']
description: 'promise'
tags: ['学习系列', 'promise']
categories: ['学习系列']
author: 'eago'
comment: true
---

promise 是异步编程方案，比回调和事件更强大

三种状态：pending，fulfilled，rejected。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态

一旦改变，就不会再变，任何时候都可以得到这个结果

promise 对象的状态改变，只有两种可能 pending->fulfilled，pending->rejected。只要这两种情况发生，状态就凝固了，不会再变了
