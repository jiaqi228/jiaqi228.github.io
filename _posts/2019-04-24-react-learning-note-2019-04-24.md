---
title: "React学习笔记：Redux - A single source of truth"
categories:
  - React
  - Learning Note
tags:
  - React
  - Learning Note
  - Redux
---

# Redux
Redux是Flux设计思想的**接近**实现（非完全实现）。

Redux对Flux进行了简化，去除了Dispatcher的设计思想，并引入了Reducer。

Redux规定States应该被管理在1个单独的对象中。这个对象中的内容是immutable的，无法被改变。对States的更新会体现在替换这些内容，而不是修改这些内容。
> 函数式编程思想：无副作用。

## 设计思想的转变
为了定义Actions，设计思想应该从“面向名词”（noun-oriented）转变成“面向动词”（verb-oriented）。即Actions是如何影响States的。

## Actions
- 只有Action可以改变States。
- 一个Action其实只是一个最少含有字段的Javascript对象。（Action Type ： 这是一个什么Action）

## Reducers
- Reducer是Javascript的Function，目的是对State Tree 进行模块化处理，即修改特定部分的State Tree。
- Reducer接收State和Action，并返回新的State。

## Store
- Store是管理State的对象。
- Redux规定所有State都应在1个Store中进行管理。
- 将Reducers绑定到Store，并使用Action进行Dispatch以管理State。
- subscribe绑定函数到Store，每次Store完成Dispatch时都会调用该函数。

## Action Creators
- 因为Actions其实只是文本数据，Action Creators可以用来创建和返回这些文本数据。