---
title: 浏览器的一帧
---

## frame in browser

![一帧](/images/frameInBrowser.png)

### 步骤
* 接受输入事件
* js执行任务队列中的回调： 参考[event loop 事件循环](https://wchfish.github.io/2023/07/06/event-loop/)
* 开始一帧
* RAF(requestAnimationFrame)
* Layout
* Paint
* RIC(RequestIdleCallback)

## 问题
* "输入事件"这一步做了什么？
* "开始一帧"这个概念的详解？
* js中触发强制渲染的时候，执行流程是什么样的？
* 一帧的整个流程都是同步的吗？

## reference
* [浏览器一帧都会干些什么？](https://fe.ecool.fun/topic-answer/4585f639-0eff-4190-9fa0-e1c0838284e8?orderBy=updateTime&order=desc&tagId=10)
