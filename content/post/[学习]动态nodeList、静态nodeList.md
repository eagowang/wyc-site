---
title: '[学习]动态nodeList、静态nodeList'
date: 2019-06-28T09:41:03+08:00
draft: false
keywords: ['学习系列']
description: '动态NodeList，静态NodeList'
tags: ['学习系列', '动态NodeList', '静态NodeList']
categories: ['学习系列']
author: 'eago'
comment: true
---

## NodeList

NodeList 是一个节点的集合，是由 Node.childNodes 和 document.querySelectorAll 返回的。

- 动态 NodeList：如果文档树中的节点树发生变化，则已存在的实时 NodeList 对象也会随之变化

<iframe width="100%" height="300" src="//jsfiddle.net/wangyc20/3jn87dgq/embedded/js,html,css,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>
