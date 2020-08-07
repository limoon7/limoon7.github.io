---
title: React Hooks 学习
date: 2020-02-26 16:40:24
category: 前端
tags: [React, React Hooks]
author: lemon
---

# 为什么出现React Hooks

1. React 需要为共享状态逻辑提供更好的原生途径。为了避开嵌套地狱。
2. 复杂组件变得难以理解
3. Hook 使你在非 class 的情况下可以使用更多的 React 特性


# Hooks API

## useState

> 在函数组件里面使用 class 的 setState

使用：

```ts
const [name, setName] = useState("rose");
```

## [useEffect](https://overreacted.io/zh-hans/a-complete-guide-to-useeffect/)

> 在函数组件里面使用 class 的生命周期函数，是所有函数的合体

使用：

```ts
// 基础使用
useEffect(()=>{
  ...
})
```

1. `useEffect`最后，加了[]就表示只第一次执行，同 `componentDidMount`

```ts
useEffect(() => {
  const users = "获取全国人民的信息()";
}, []);
```

2. `useEffect`最后，加[]，并且[]里面加入了字段，就表示这个字段更改了，当前`effect`才执行

```ts
useEffect(() => {
  const users = "(name改变了我才获取全国人民的信息())";
}, [name]);
```

3. `useEffect`最后，不加[]就表示每一次渲染都执行，用于替代每次渲染都会执行的生命周期函数，如 `willUpdate`

```ts
useEffect(() => {
  const users = "每次都获取全国人民的信息()";
});
```

4. 在`effect`的`return`里面可以做取消订阅的事,用于替代`willUnmount`

```ts
useEffect(() => {
  const subscription = "订阅全国人民吃饭的情报！";
  return () => {
    "取消订阅全国人民吃饭的情报！";
  };
}, []);
```

> 为什么要取消订阅？
>
> 大家都知道，render 了之后会执行重新 useEffect，如果 useEffect 里面有一个 setInterval...那么每次 render 了，再次执行 useEffect 就会再创建一个 setInterval，然后就混乱了

5. useEffect 里面使用到的 state 的值, 固定在了 useEffect 内部， 不会被改变，除非 useEffect 刷新，重新固定 state 的值

```ts
const [count, setCount] = useState(0);
useEffect(() => {
  console.log("use effect...", count);
  const timer = setInterval(() => {
    console.log("timer...count:", count);
    setCount(count + 1);
  }, 1000);
  return () => clearInterval(timer);
}, []);
```

6. useEffect 不能被判断包裹
7. useEffect 不能被打断 (后期看文档)

## useRef

> 相当于全局作用域，一处被修改，其他地方全更新...

使用：

```ts
const countRef = useRef(0);
```

1. 普遍操作，用来操作 dom

```ts
const Hook = () => {
  const [count, setCount] = useState(0);
  const btnRef = useRef(null);

  useEffect(() => {
    console.log("use effect...");
    const onClick = () => {
      setCount(count + 1);
    };
    btnRef.current.addEventListener("click", onClick, false);
    return () => btnRef.current.removeEventListener("click", onClick, false);
  }, [count]);

  return (
    <div>
      <div>{count}</div>
      <button ref={btnRef}>click me </button>
    </div>
  );
};
```

## useMemo

1. memo 的用法是：与函数组件里面的`PureComponent`异同，都是对接收的props参数进行浅比较，解决组件在运行时的效率问题，优化组件的重渲染行为。但是，如果函数组件被 React.memo 包裹，且其实现中拥有 useState 或 useContext 的 Hook，当 context 发生变化时，它仍会重新渲染。
2. memo是浅比较，意思是，对象只比较内存地址，只要你内存地址没变，管你对象里面的值千变万化都不会触发render
3. React.memo()是判断一个函数组件的渲染是否重复执行。useMemo()是定义一段函数逻辑是否重复执行。useMemo 解决了值的缓存的问题。

## useCallback

1. useMemo 与 useCallback 类似，都是有着缓存的作用。本质的区别可能就是：useMemo 是缓存值的。useCallback 是缓存函数的
2. 没有依赖，添加空的依赖，就是空数组！

## useReducer

使用redux中存储的数据

