---
title: '[Git]git学习（三）'
date: 2019-07-23T08:36:27+08:00
draft: true
---

## 分支简介

Git 保存的不是文件的变化或差异，而是一系列不同时刻的文件快照。

在进行提交操作时，Git 会保存一个提交对象。包含一个指向内容快照的指针，还包含姓名、邮箱、提交信息、以及指向父对象的指针。

结构如下：
![img](https://git-scm.com/book/en/v2/images/commit-and-tree.png)

## 创建分支

Git 的分支，本质上仅仅是指向提交对象的可变指针

```
git branch testing
```

![img](https://git-scm.com/book/en/v2/images/head-to-master.png)

上面创建了 testing 分支，HEAD 表示当前分支

## 分支切换

```
git checkout testing
```

![img](https://git-scm.com/book/en/v2/images/head-to-testing.png)
