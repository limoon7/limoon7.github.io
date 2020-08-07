---
title: TypeScript 泛型学习
date: 2019-08-06 08:30:29
category: 前端
tags: typeScript
author: lemon
---


![泛型](https://tva1.sinaimg.cn/large/007S8ZIlly1gfvpewnitlj30zk0bp0t8.jpg)

[参考文章](https://juejin.im/post/5ee00fca51882536846781ee#heading-0)

# 泛型

## 泛型是什么

设计泛型的关键目的是在成员之间提供有意义的约束，这些成员可以是：类的实例成员、类的方法、函数参数和函数返回值。

## 泛型接口

```js

interface Identities<V,M> {
  value: V;
  message: M;
}

identity<T, U> (value: T, message: U): Identities<T, U> {
  console.log(value + ": " + typeof (value));
  console.log(message + ": " + typeof (message));
  let identities: Identities<T, U> = {
    value,
    message
  };
  return identities;
}

this.identity('111111111', 1)
```

## 泛型类

我们在什么时候需要使用泛型呢？通常在决定是否使用泛型时，我们有以下两个参考标准：

1. 当你的函数、接口或类将处理多种数据类型时；
2. 当函数、接口或类在多个地方使用该数据类型时。

## 泛型约束

1. 确保属性存在
2. 检查对象上的键是否存在

## 泛型参数默认类型

1. 有默认类型的类型参数被认为是可选的。
2. 必选的类型参数不能在可选的类型参数后。
3. 如果类型参数有约束，类型参数的默认类型必须满足这个约束。
4. 当指定类型实参时，你只需要指定必选类型参数的类型实参。 未指定的类型参数会被解析为它们的默认类型。
5. 如果指定了默认类型，且类型推断无法选择一个候选类型，那么将使用默认类型作为推断结果。
6. 一个被现有类或接口合并的类或者接口的声明可以为现有类型参数引入默认类型。
7. 一个被现有类或接口合并的类或者接口的声明可以引入新的类型参数，只要它指定了默认类型。


## 泛型工具类型

1. Partial<T> 的作用就是将某个类型里的属性全部变为可选项 ?。
2. Record<K extends keyof any, T> 的作用是将 K 中所有的属性的值转化为 T 类型。
3. Pick<T, K extends keyof T> 的作用是将某个类型中的子属性挑出来，变成包含这个类型部分属性的子类型。
4. Exclude<T, U> 的作用是将某个类型中属于另一个的类型移除掉。
5. ReturnType<T> 的作用是用于获取函数 T 的返回类型。


项目中不一定要强制使用泛型，还是应该用在对的场景。