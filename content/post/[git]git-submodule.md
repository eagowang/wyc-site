---
title: "[Git]Git Submodule"
author: "eago"
tags: ["git"]
categories: ["git"]
date: 2019-05-30T17:08:10+08:00
draft: false
---

场景描述：比如这个 hugo 博客，整个博客是一个 git 仓库，生成的 public 文件对应一个 git 仓库

## 添加子模块

在项目根目录

```
git add submodule git@github.com:eagowang/eagowang.github.io.git public
```

这条命令会自动 clone，并生成一个.gitmodules 文件，内容如下

```
[submodule "public"]
	path = public
	url = git@github.com:eagowang/eagowang.github.io.git

```

## 更新子模块

有时，子模块是单独开发的，需要拉取最新代码

1. 在 submodule 目录下，更新操作无异
2. 在根目录下，可以使用如下命令

```
git submodule update --remote public
```

## 提交子模块

进入子模块，然后正常提交

## 删除子模块

1. 先删除对应的文件

```
// 删除暂存区上的文件
git rm --cached public
// 删除文件
rm -rf public
// 删除.gitmodules文件
rm .gitmodules
```

2. 更改 git/config，删掉 submodule 相关信息

```
vim .git/config
```
