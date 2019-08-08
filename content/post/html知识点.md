---
title: "html知识点"
date: 2019-06-12T09:58:58+08:00
author: "eago"
tags: ["html"]
categories: ["html"]
draft: false
---

## doctype

doctype 声明不是 html 标签，用来告诉浏览器当前页面使用哪种 html 版本

- html4.01 中，需要引入 dtd（文档类型声明），因为 html4.01 基于 SGML（standard generalized markup language，标准通用标记语言）。dtd 指定了标记语言的规则，确保了浏览器能够正确渲染内容

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

- html5 不基于 SGML，因此不要求引用 dtd

```html
<!DOCTYPE html>
```

## meta 标签

提供页面有关的元信息

| 属性       | 值                                                                          | 描述                            |
| ---------- | --------------------------------------------------------------------------- | ------------------------------- |
| http-equiv | content-type <br/> expires <br/>refresh<br/>set-cookie                      | 把 content 属性关联到 HTTP 头部 |
| name       | author <br/> description <br/>keywords<br/>generator<br/>revised<br/>others | 把 content 内容关联到一个名称   |
| scheme     | some_text                                                                   | 定义用于翻译 content 属性的格式 |

1.name 属性

比较常用的比如 keywords,比如这篇文章的 meta 标签如下

```html
<meta name="keywords" content="HTML,学习系列" />
```

搜索引擎就会根据我提供的关键字进行分类

其他还有：

- referrer：referrer 首部
- viewport：仅供移动设备使用

  2.http-equiv 属性

告诉服务器在发送实际的文档之前先在要传送给浏览器的 MIME 文档头部包含名称/值对

例如：

```html
<meta http-equiv="charset" content="iso-8859-1" />
<meta http-equiv="expires" content="31 Dec 2008" />
```

发送到浏览器的 header 就是这样：

```
content-type: text/html
charset:iso-8859-1
expires:31 Dec 2008
```

3.一些 meta 标签

(1) 浏览器 csp 策略

```html
<meta
  http-equiv="Content-Security-Policy"
  content="upgrade-insecure-requests"
/>
```

(2) 控制浏览器的 DNS 预读取功能

```html
<meta http-equiv="x-dns-prefetch-control" content="on" />
```

(3) ios 删除苹果默认的工具栏和菜单栏，来给用户腾出更多的空间从而让网页得到更好的展现，让 iphone 达到屏幕增大的效果。

```html
<meta name="apple-mobile-web-app-capable" content="yes" />
```

(4) ios 控制状态栏显示样式

```html
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
```

(5) ios 手机号码不被显示为拨号链接

````html
<meta name="format-detection" content="telephone=no" />
ios``` ## script 标签 ### 常规用法 1.外部脚本（src） ```html
<script src="script.js"></script>
````

2.内嵌脚本

```html
<script type="text/javascript">
  document.write("Hello World!");
</script>
```

### async 和 defer

> 默认情况：浏览器同步下载和执行 js 脚本

- async

      在 html parsing 阶段异步下载脚本，下载完成之后立即执行

- defer

      在 html parsing 阶段异步下载脚本，但是延迟执行脚本（在 html parsing 结束之后）,多个 defer 脚本不一定会按顺序执行

图示：

![image](https://image-static.segmentfault.com/28/4a/284aec5bb7f16b3ef4e7482110c5ddbb_articlex)

> 使用场景：（更好的利用异步下载特性）
>
> 1. 一般情况下，我们都会把脚本放在\<body>结束之前，但是对于一些需要放在 header 中提前执行，且无依赖的脚本，就可以使用 async
>
> 2. 对于不需要提前执行且无依赖的异步脚本也可以放在 header 中，使用 defer

## 语义化标签

html5 之前，人们常说 div+css。所以全网站都是 div+span。html5，可以使用\<article>、\<section>、\<nav>、\<aside>、\<header>、\<footer>等看名字就能判断出内容的标签
