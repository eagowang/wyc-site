---
title: 'Refs和refs转发'
date: 2019-06-07T09:42:24+08:00
draft: false
keywords: ['react', 'refs', 'refs转发']
description: 'refs和refs转发'
tags: ['react']
categories: ['前端', 'react']
author: 'eago'
comment: true
---

## refs

使用 Refs 可以访问 dom 节点

### 何时使用 refs

几种适合使用 refs 的情况：

1. 管理焦点（焦点没法通过 state 控制）
2. 触发强制动画
3. 集成第三方 dom 库

### createRef

```jsx
class Input extends Component {
  constructor() {
    this.inputRef = React.createRef();
  }
  componentDidMount() {
    this.inputRef.current.focus();
  }
  render() {
    return <input ref={this.inputRef} />;
  }
}
```

### 回调 ref

```jsx
class Input extends Component {
  constructor() {}
  componentDidMount() {
    this.inputRef.current.focus();
  }
  render() {
    return <input ref={e => (this.inputRef = e)} />;
  }
}
```

### useRef(react hooks)

```jsx
function HookInput() {
  const inputRef = useRef(null);
  useEffect(() => {
    inputRef.current.focus();
  }, []);
  return <input ref={inputRef} type="text" />;
}
```

## refs 转发

### 什么是 refs 转发

refs 转发是一项将 ref 转发到其子组件的技巧。

### 什么情况用 refs 转发

refs 转发通常用于写一些可重用的组件。（封装后的组件调用需要操作底层 dom）

### 基本用法

1. forwardRef

```jsx
const Input = React.forwardRef((props, ref) => {
  return <input ref={ref} defaultValue={props.defaultValue} />;
});

//...
const inputRef = React.createRef();
//...
<Input ref={this.inputRef} />;
```

2. 使用特定名字的 props 传递（在没有 forwardRef 之前）

```jsx
function Input(props){
  const {forwardRef, ...rest} = props;
  return <input ref={forwardRef}/ {...rest}/>
}

//...
const inputRef = React.createRef();
// ...
this.input
<Input forwardRef={this.inputRef}>
```

## 高阶组件使用 refs 转发

注意：refs 将不会透传下去。这是因为 ref 不是 prop 属性。就像 key 一样，其被 React 进行了特殊处理。如果你对 HOC 添加 ref，该 ref 将引用最外层的容器组件，而不是被包裹的组件。

```jsx
function inputWrap(Component) {
  class InputWrap extends React.Component {
    componentDidMount() {
      console.log(this.props);
    }
    render() {
      const { forwardRef, ...rest } = this.props;
      return <Component ref={forwardRef} {...rest} />;
    }
  }

  return React.forwardRef((props, ref) => {
    return <InputWrap forwardRef={ref} />;
  });
}
```
