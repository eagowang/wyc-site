---
title: "[git]git（一）"
author: "eago"
tags: ["git"]
categories: ["git"]
date: 2019-07-22T13:58:29+08:00
draft: false
---

**注**:内容全部为[git pro](https://git-scm.com/book/zh/v2/)摘要

我大概知道这些命令

```js
// 提交
git add
git commit
git push
// 拉取
git clone
git pull
git fetch
git merge
// 分支
git checkout
git branch
git tag
```

日常工作是基本可以满足的，但是在分支合并出了什么岔子的时候往往一脸懵逼

## 分布式

客户端不只是提取最新版本的文件快照，而是把代码仓库完整的镜像下来。

## 与其它版本工具的区别

1. 对待数据的方法：其他大部分系统以文件变更列表的方式存储信息。这类系统将它们保存的信息看作是一组基本文件和每个文件随时间逐步积累的差异。Git 把数据看作是对小型文件系统的一组快照。每次提交更新，或在 Git 中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。

2. 近乎所有的操作都是本地执行
3. 保证完整性：Git 中所有数据在存储之前都计算校验和，然后以校验和来引用。这意味着不可能在 Git 不知情时更改任何文件内容或目录
4. Git 一般只添加数据

## 三种状态

Git 有三种状态，文件可能处于其中之一：已提交（committed），已修改（modifed）和已暂存（staged）。

## 三个工作区域

由三种状态引入三个工作区域的概念：Git 仓库、工作目录以及暂存区域。

![img](https://git-scm.com/book/en/v2/images/areas.png)

- Git 仓库：保存项目的元数据和对象数据库的地方。这是 Git 中最重要的部分，从其他计算机克隆仓库时，拷贝的就是这里的数据
- 工作目录是对项目的某个版本独立提取出来的内容。
- 暂存区：是一个文件，保存了下次将提交的文件列表信息，一般在 Git 仓库目录中。有时也叫“索引”

## 初次运行 Git 前的配置

Git 自带一个`git config`的工具来帮助设置控制 Git 外观和行为的配置变量。

- `--system`所有用户的通用配置
- `--global`当前用户的通用配置
- 当前使用仓库的 Git 目录中的 config 文件（就是 .git/config）：针对该仓库。

```
git config --list
git config user.name
git config --global user.email haha@example.com
git config --global user.name "haha"
```
