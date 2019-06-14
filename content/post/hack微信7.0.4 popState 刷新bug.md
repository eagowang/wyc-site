---
title: 'Hack微信7.0.4 popState 刷新bug'
date: 2019-05-23T11:40:44+08:00
draft: false
keywords: ['popState', '微信开发']
description: '微信popState刷新bug'
tags: ['popState', '微信']
categories: ['前端']
author: 'eago'
comment: true
---

原因：业务要求需要 pushState 一次

探索：发现微信 pushState 两次，且两次带上不同的 hash，再回退，不会有刷新

解决办法：

```
componentDidMount(){
  window.history.replaceState({fix: true}, '', '#fix')
}
```

具体问题描述看：
[安卓微信 v7.0.4，触发 popState 网页会刷新](https://developers.weixin.qq.com/community/develop/doc/000c2a75e20a686fd76879bc651800?jumpto=reply&parent_commentid=000a44a1b185e0efdb686c39353c&commentid=000eaaf26149e833d088763e2518)
