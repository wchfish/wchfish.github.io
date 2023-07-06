---
title: react渲染原理
---

## 问题
* react在渲染时解决了哪些问题？做了什么，怎样实现的？
* Fiber架构与老的stack架构区别是什么？

## 原理
### 触发渲染的流程
EventTrigger -> handler into task queue -> call stack execute hanler -> [update state, trigger effect, ...] -> react render

### 首次渲染 react element -> VDOM -> DOM
* DOM节点: 通过Document.createElement创建真实DOM；递归遍历children属性，创建DOM节点。
* 函数组件节点：调用函数，递归处理返回值。
* 类组件节点：
    1. constructor创建实例
    2. 调用render,返回值 -> VDOM树
    3. 调用didMount方法
* 数组节点：遍历数组项并处理

### 更新
* 组件更新：
    1. shouldComponentUpdate
    2. render,得到新的VDOM树，与snapshot做对比更新
    3. didUpdate加入队列（应该是macroTaskQueue），等待将来执行
    4. 重新生成VDOM树
    5. 更新真实DOM
    6. 执行队列，包括didMount，didUpdate，willUnMount

## 相关概念
* ReactElement: react元素，react对UI元素的抽象。组件实例与ReactElement对应，无论是类组件还是函数组件。
* VDOM Tree：虚拟节点，react在js运行时中对DOM树的抽象。react通过对比VNode Tree的快照，决定DOM的更新方式。
* Fiber: react新的架构，在框架层面对渲染机制做了优化。支持异步渲染。
* hooks：react通过hooks对函数组件的能力进行加强，使函数组件有自己的state、effect等特性。
* event loop: browser实现的事件驱动模型, 任务队列分为MicroTask和MaCroTask。
* 调度算法：react更新UI的schedule

### VDOM
虚拟节点类型
* dom节点
* 组件节点
* 文本节点
* 空节点  
* 数组节点

## 运用及检验
* 描述react页面初次渲染时的过程。
* 描述react页面更新过程，包括用户交互（点击）、网络请求等行为触发的更新。以及有多个state需要更新时的执行过程。

## 延伸
* 基于react渲染原理的性能优化方案
    1. 由于组件的render方法默认会递归的调用子组件的render函数，所以组件更新时应该尽可能只触发必要的render。
    2. 基于react diff更新真实dom的算法，应该提高dom元素的复用率，比如数组元素加key，保持组件结构的稳定等。

## reference
* [「万字总结」🍒动画 + 大白话讲清楚React渲染原理](https://juejin.cn/post/7121378029682556958)
    
    内容：
    1. 类组件的生命周期有哪些，作用是什么
    2. react element是什么; VDOM节点类型有哪些？
    3. 首次渲染过程；组件更新的步骤；
    4. diff方式及DOM更新的方式
    
    问题：
    1. setState在react中是如何触发组件更新的？是同步还是异步，是否有batch处理？
    2. 组件的render返回结果是否就是VDom子树？render是否会同步调用子组件的render方法，依赖子组件的render返回值？
    3. react是怎么保证didMount/didUpdate方法在DOM更新以后执行的？
    4. react更新真实DOM的细节
* event loop: todo add link