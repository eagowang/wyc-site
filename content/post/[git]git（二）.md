---
title: "[Git]git（二）"
author: "eago"
tags: ["git"]
categories: ["git"]
date: 2019-07-22T15:49:08+08:00
draft: false
---

## 获取仓库

- `git init`
- `git clone`

## 记录每次更新到仓库

工作目录下的每一个文件都不外乎这两种状态：已跟踪或未跟踪。

- 已跟踪：已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后，他们的状态可能处于未修改，已修改或已放入暂存区。
- 未跟踪：工作目录中除已跟踪文件以外的所有其它文件都属于未跟踪文件，它们既不存在于上次快照的记录中，也没有放入暂存区。

![img](https://git-scm.com/book/en/v2/images/lifecycle.png)

## 检查当前文件状态

```
git status
// 概览
git status -s
```

## 忽略文件

使用.gitignore 文件

规范：

- 所有空行或以#开头的行都会被 Git 忽略
- 可以使用标准的 glob 模式匹配
- 匹配模式可以以（/）开头防止递归
- 匹配模式可以以（/）结尾指定目录
- 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反

## 查看已暂存和未暂存的修改

- 查看未暂存的修改`git diff`
- 查看已暂存的修改`git diff --staged`

## 提交

```
git commit "提交"
git commit -am "跳过缓存区提交"
```

## 移除文件

```
// 取消跟踪，并移除文件
git rm xxx
// 取消跟踪，并移除文件（保留工作区）
git rm --cached xxx
```

## 移动文件

```
// 重命名
git mv readme.md README.md
// 相当于运行了以下三条命令
mv readme.md README.md
git rm readme.md
git add README.md
```

## 查看提交历史

```
// 会列出每个提交的sha-1检验和、作者名字、邮箱、提交时间
// 和说明
git log
```

格式化选项

`--pretty`可选的值 oneline，short，full，fuller，format。

```
// format 格式化，graph 图形化
git log --pretty=format:"%h - %an, %ar : %s" --graph
```

限制 git log 输出的选项

```
// 包含指定关键字的提交
git log --grep "xx"
// -p 显示每次提交的差异， -2 表示最近两次提交
git log -p -2
// --stat 每次提交的简略统计信息
git log --stat
```

## 撤销操作

在任何阶段，都可能想要撤销某些操作

```
// 重新提交
git commit --amend
// 取消暂存的文件
git reset HEAD README.md
// 取消未暂存的文件
git checkout README.md
```

## 远程仓库的使用

管理远程仓库包括了解如何添加远程仓库、移除无效的远程仓库、管理不同的远程分支并定义它们是否被跟踪等等。

## 查看远程仓库

```
// 查看远程服务器的简写
git remote
// 查看远程服务器简写及其url
git remote -v
```

## 添加远程仓库

```
git remote add origin git@github.com:eagowang/wyc-site.git
```

## 从远程仓库抓取或拉取

```
// 拉取数据到本地仓库，但不会自动合并或修改当前的工作
git fetch origin
// 抓取然后合并远程分支到当前分支
git pull
```

## 推送到远程仓库

```
git push origin master
```

## 查看远程仓库信息

```
git remote show origin
```

## 远程仓库的移除与重命名

```
// 重命名
git remote rename origin wyc_site
// 移除
git remote rm origin
```

## 打标签

- 轻量标签：只是特定提交的引用
- 附注标签：存储在 Git 数据库中的一个完整对象。（其中包含打标签者的名字、电子邮件地址、日期时间；还有一个标签信息；）

```
// 附注标签
git tag -a v1.0.0 -m "my version 1.0.0"
// 查看标签
git tag
// 查看标签信息
git show v1.0.0
// 轻量标签
git tag v1.0.1
// 删除标签
git tag -d v1.0.1
// 给某一次提交打标签
git tag -a v1.0.2 9fceb02
// 推送标签
git push origin v1.0.2
git push origin --tags
// 检出标签
git checkout v1.0.2
// 根据标签创建新愤怒值
git checkout -b v1.0.3 v1.0.2
```

## Git 别名

```
git config --global alias.co checkout
```
