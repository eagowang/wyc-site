---
title: "使用hugo搭建个人博客"
author: "eago"
tags: ["hugo"]
date: 2019-05-23T11:10:15+08:00
draft: false
---

## hugo 命令

1. 创建一篇新博客

```
hugo new post/xxx.md
```

2. 本地运行 hugo server

```
hugo server --buildDrafts --watch
```

3. 部署

```
hugo --baseUrl="http://eagowang.github.io"
```
