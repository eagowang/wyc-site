---
title: '[学习]css知识点'
date: 2019-06-12T13:46:55+08:00
draft: false
keywords: ['学习系列']
description: 'css知识点'
tags: ['学习系列', 'css']
categories: ['学习系列', 'css']
author: 'eago'
comment: true
---

## 基础

### 盒子模型

margin,border,padding,content(外边距，边框，内边距，内容)

![image](<https://mdn.mozillademos.org/files/8685/boxmodel-(3).png>)

> 常说的元素的 width，height 指的是 content 的宽度和高度。这跟我们的潜意识不符，可以用 box-sizing 属性来修改（border-box,content-box）

### 选择器

常用的：

1.id,class,元素，后代

```css
/*id*/
#wrap {
}
/*class*/
.main {
}
/*元素*/
body {
}
/*后代*/
table tr {
}
```

2.伪类选择器

伪类选择器，表现为给这个元素加一个类（伪类）,用单冒号:

- :link
- :visited
- :hover
- :active
- :focus
- :first-child
- :last-child
- :nth-child

例子：(顺序不能变)

```css
a:link {
  color: red;
}
a:visited {
  color: green;
}
a:hover {
  color: yellow;
}
a:active {
  color: pink;
}
```

3.伪元素选择器
伪元素选择器，表现为加一个元素（伪元素）,用双冒号::

- ::before
- ::after
- ::first-letter

例子：(title 前面添加一个小方块)

```css
.main::before {
  display: block;
  content: '';
  width: 2px;
  height: 12px;
  background: orange;
}
```

### 优先级

首先，内联样式>外部样式（也就是 style 最大）

其次，不同选择器的优先级也不同：

1. 元素选择器，伪元素选择器（权重 1）
2. 类选择器，属性选择器，伪类选择器（权重 10）
3. id 选择器（权重 100）

!important 例外，当一个样式声明的!important 时，此声明将覆盖其他任何声明。（!imortant 不能乱用）

总结：

> !important>行内样式>ID 选择器 > 类选择器 | 属性选择器 | 伪类选择器 > 元素选择器

### css 动画

#### transition

过渡，只能定义起止状态，而且需要特定的触发时机，比如:hover，或者动态添加 class 或者 style

使用方式：property name | duration | timing function | delay

```css
.a:hover {
  transition: margin-right 4s ease-in-out 1s;
}
```

#### animation

animation 可以设置动画的多个状态（不只是起止，使用%）,不需要特定的触发时机。还可以设置循环次数，动画方向，动画结束状态

使用方式： name | duration | timing-function | delay |
iteration-count | direction | fill-mode | play-state

```css
.block {
  animation: slidein 1s linear 1s infinite normal forwards;
}

@keyframes slidein {
  from: {
    margin-left: 0;
  }
  to: {
    margin-left: 100px;
  }
}
```

### 浮动和清除浮动

以前使用浮动，主要是为了自适应布局（左浮动，右浮动，中间自适应）

```css
.wrap {
  overflow: hidden;
  margin: 0;
  padding: 0;
}
.left {
  float: left;
  background: cadetblue;
  width: 100px;
  height: 100px;
}
.right {
  float: right;
  background: rebeccapurple;
  width: 100px;
  height: 100px;
}
.mid {
  background: chartreuse;
  height: 100px;
  margin-left: 110px;
  margin-right: 110px;
}
```

```html
<div class="wrap">
  <div class="left"></div>
  <div class="right"></div>
  <div class="mid"></div>
</div>
```

#### 清除浮动

1. clear:both

给最后一个不浮动的元素加上 clear:both，没有就加一个空元素

```css
.clear {
  clear: both;
}
```

2. bfc 清除浮动

```css
.wrap {
  overflow: hidden;
  /*overflow: auto;*/
  /*position: absolute;*/
}
```

### flex 布局

[Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

这篇已经写的很好了，看看如何实现上面说的三列中间自适应的布局

#### 三列中间自适应

```css
.wrap {
  display: flex;
}
.left {
  width: 100px;
  height: 100px;
  background: cadetblue;
}
.mid {
  flex: 1;
  height: 100px;
  background: darkblue;
}
.right {
  width: 100px;
  height: 100px;
  background: violet;
}
```

```html
<div class="wrap">
  <div class="left"></div>
  <div class="right"></div>
  <div class="mid"></div>
</div>
```

#### 水平垂直居中

```css
.wrap {
  display: flex;
  justify-content: cenrer;
  align-items: center;
}
```

#### 多个元素水平均匀分布

```css
.wrap {
  display: flex;
  justify-content: space-between;
  /* justify-content: space-around; */
}
```

### ifc 和 bfc

#### bfc

bfc，是一个独立的渲染区域，只有块级元素参与，规定内部的块级元素如何布局

bfc 规则：

1. 内部的 box 会在垂直方向，一个接一个的放置
2. box 垂直方向的距离有 margin 决定。同属一个 bfc 的两个相邻 box 会发生 margin 重叠
3. 每个元素的 margin-box 左边，与包含块的 border-box 接触。即使存在浮动也是如此
4. bfc 的区域不会与 float-box 重叠
5. bfc 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
6. 计算 bfc 的高度时，浮动元素也参与计算

有时，我们会利用 bfc 清除 margin 重叠，清除浮动，bfc 怎么生成呢？

1. 根元素或者包含根的元素
2. 浮动元素（float 不为 none）
3. display 为 inline-block,flex,flow-root(新)的元素
4. 绝对定位元素（position 为 absolute 或 fixed）

#### ifc

规定行内元素如何布局

ifc 规则：

1. 行内元素从容器的顶端开始，一个接一个水平布局
2. 水平 padding,border,margin 有效。垂直无效
3. 一个水平行中所有 inline-box 组成 line-box 的矩形区域，其高度就是容器的高度

### line-height

[深入理解 CSS：字体度量、line-height 和 vertical-aligns](https://zhuanlan.zhihu.com/p/25808995)

### z-index 和层叠上下文

#### z-index

z-index 设置属性在 z 轴的显示层级。通常来说 z-index 大的元素会覆盖小的元素

对于一个已经定位的元素（position 不是 static）的元素，z-index 属性指定：

1. 元素在当前层叠上下文的层级
2. 创建一个新的层叠上下文

#### 层叠上下文

[深入理解 CSS 中的层叠上下文和层叠顺序](https://www.zhangxinxu.com/wordpress/2016/01/understand-css-stacking-context-order-z-index/)

上面 z-index 说到了层叠上下文，一个是指定当前层级，一个是创建层叠上下文。
层叠上下文可以理解为一个封闭区域，同一层级的层叠上下文做对比

创建层叠上下文：

1. 根元素（HTML）
2. z-index 值不为 auto 的绝对定位/相对定位
3. 一个 z-index 值不为 auto 的 flex 项目 (flex item)，即：父元素 display: flex|inline-flex
4. opacity 值小于 1 的元素（opcacity 元素不能设置 z-index，相当于 z-index=0）
5. filter 不为 none 的元素
6. perspective 值不为 none 的元素
7. position: fixed
8. -webkit-overflow-scrolling: touch

### clientWidth,offsetWidth,innerWidth

![image](https://i.stack.imgur.com/Cl1IA.png)

## 扩展

### css 预处理器

可以理解为 css 上层语言，可以编译成 css。

常用的有 less，scss，可以使用一高级语法，比如嵌套，变量，函数等

### css 后处理器

可以理解为直接处理 css 文件

postcss，一般用在 wepack 中，作为一个 loader，常用的功能有 css 兼容，rem 转换等
