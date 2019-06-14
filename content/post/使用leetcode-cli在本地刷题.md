---
title: '使用leetcode'
date: 2019-05-30T20:16:41+08:00
draft: true
keywords: ['leetcode-cli', 'leetcode']
description: '使用leetcode-cli在本地刷题'
tags: ['leetcode', 'leetcode-cli']
categories: ['前端', '算法']
author: 'eago'
comment: true
---

使用 leetcode-cli 本地刷题

## 安装

## 登陆

## 选题

1. 查看问题列表

```js
// 全部列表
leetcode list
//查看简单问题列表
leetcode list -q e
```

2. 筛选题

```js
// 随机简单一题
leetcode show -q e
// 查看指定题
leetcode show 104
```

3. 生成并打开文件

```js
leetcode show 104 -gxe -l javascript
```

## 测试

```js
leetcode test 538.convert-bst-to-greater-tree.js
```

## 提交

```js
leetcode submit 538.convert-bst-to-greater-tree.js
```
