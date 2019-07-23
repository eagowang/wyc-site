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
// 切换testing分支
git checkout testing
```

![img](https://git-scm.com/book/en/v2/images/head-to-testing.png)

做些修改在 testing 分支提交

![img](https://git-scm.com/book/en/v2/images/advance-testing.png)

回到 master 分支

```
git checkout master
```

![img](https://git-scm.com/book/en/v2/images/checkout-master.png)

做些修改，在 master 分支提交
![img](https://git-scm.com/book/en/v2/images/advance-master.png)

这时，提交历史已经产生了分叉。查看一下分叉历史

```
git log --oneline --decorate --graph --all
```

## 分支合并

- 没有分歧的合并：当你试图合并两个分支时，如果顺着一个分支走下去能到达另一个分支，那么 Git 在合并两者的时候，只会简单的将指针向前推进——fast-forward（快进）
- 有分歧的合并：Git 会使用两个分支的末端所指的快照以及这两个分支的祖先，做一个简单的三方合并。和 fast-forward 不同的是，Git 将此次三方合并的结果做了一个新的快照并且自动创建一个新的提交指向它。这个被称作一次合并提交，它的特别之处在于他有不止一个父提交。

![img](https://git-scm.com/book/en/v2/images/basic-merging-1.png)
![img](https://git-scm.com/book/en/v2/images/basic-merging-2.png)
