---
title: react-redux 学习
date: 2019-07-31 10:48:14
category: 前端
tags: [React, redux]
author: lemon
---

# 关于`mapStateToProps和mapDispatchToProps`

理解：从store中获取信息上升到props中，这样就有两种props，一种是组件本身的，一种是从store中获取的。

[参考](https://www.imweb.io/topic/5a426d32a192c3b460fce354)

## `mapStateToProps(state,ownProps)` 

`mapStateToProps`是一个函数，用于建立组件跟`store`和`state`的映射关系，作为一个函数，它可以传入两个参数，结果一定要返回一个`object`

传入`mapStateToProps`之后，会订阅`store`的状态改变，在每次`store`的`state`发生变化的时候，都会被调用。

`ownProps`代表组件本身的`props`，如果写了第二个参数`ownProps`，那么当`prop`发生变化的时候，`mapStateToProps`也会被调用。例如，当 `props`接收到来自父组件一个小小的改动，那么你所使用的 `ownProps`参数，`mapStateToProps` 都会被重新计算

`mapStateToProps`可以不传，如果不传，组件不会监听`store`的变化，也就是说`store`的更新不会引起UI的更新

example:

```
const mapStateToProps = (state) => {
  return {
    todoList: state.todoList
  }
}

传入了props的：

const mapStateToProps = (state, ownProps) => {
  return {
    active: ownProps.filter === state.visibilityFilter
  }
}
```

## `mapDispatchToProps`

```
mapDispatchToProps用于建立组件跟store.dispatch的映射关系

可以是一个object，也可以传入函数

如果mapDispatchToProps是一个函数，它可以传入dispatch,ownProps, 定义UI组件如何发出action，实际上就是要调用dispatch这个方法
```