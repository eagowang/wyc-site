---
title: 'React受控组件和非受控组件'
date: 2019-06-08T11:23:07+08:00
draft: false
keywords: ['react', '受控组件', '非受控组件']
description: 'react受控组件和非受控组件'
tags: ['react']
categories: ['前端', 'react']
author: 'eago'
comment: true
---

- 受控组件：用 state 控制取值的表单输入元素叫做受控组件

- 非受控组件：使用 dom 节点控制取值的表单输入元素

## 什么时候使用受控组件，非受控组件

原文：[controlled-vs-uncontrolled-inputs-react](https://goshakkk.name/controlled-vs-uncontrolled-inputs-react/)

## 简单总结：

1. 当表单功能比较简单时（或者只需要表单提交时验证）就可以使用非受控组件。
2. 当表单功能复杂时，不停的输入验证，条件控制提交按钮，强制输入格式，动态输入时，就需要用到受控组件了
