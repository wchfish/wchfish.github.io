---
title: 事件循环(Event Loop)
---

## 现代浏览器中的事件循环
### 循环过程
... -> one macro task -> all micro task -> UI render -> ...

### trigger
* macro: setTimeout, setInterval, browser event handler
* micro: queueMicrotask, promise

## Node中的事件循环


## reference
* [事件循环：微任务和宏任务](https://zh.javascript.info/event-loop)
* [并发模型与事件循环](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Event_loop)
