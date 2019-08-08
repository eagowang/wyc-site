---
title: "[React]React封装下拉选择框"
author: "eago"
tags: ["react", "组件封装"]
categories: ["react"]
date: 2019-05-30T20:03:14+08:00
draft: true
---

antd 的 select 组件使用方式如下：

```jsx
<Select defaultValue="1" onChange={}>
  <Option value="1">选项1</Option>
  <Option value="2">选项2</Option>
  <Option value="3">选项3</Option>
</Select>
```

1. 不难看出 Option 作为 Select 的 children 渲染，

2. 使用 context 传递数据和方法
