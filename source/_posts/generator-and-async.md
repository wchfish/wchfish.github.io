---
title: 生成器与异步函数
---

## 一、生成器函数

* 调用生成器函数会创建一个生成器的迭代器对象
* 生成器函数支持函数执行的暂停和恢复，gen.next()方法从上次暂停位置执行到遇到的第一个yield表达式，并把yield右侧表达式的执行结果作为next返回的{ value }。
* return会结束生成器函数，即next返回{ done: true }。
* js使用协程实现生成器函数。next和yield语句会切换主线程的控制权。


## async/await
async/await利用生成器和promise实现自身的功能，即利用协程和微任务实现了异步函数。


## 附录：reference
* [JavaScript引擎是如何实现async/await的](https://cloud.tencent.com/developer/article/1965452)
* [function*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/function*)
* [JavaScript中的Generator函数](https://cloud.tencent.com/developer/article/2305490?areaId=106001)
* [Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)
