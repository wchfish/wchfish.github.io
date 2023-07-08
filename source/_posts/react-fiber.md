---
title: react fiber 架构解析
---

## 相关概念
* MessageChannel

## reference
* [前端工程师的自我修养：React Fiber 是如何实现更新过程可控的](https://www.infoq.cn/article/flex4gdzigdmjueq4orw)
    
    内容：对fiber的概念没有解释清楚，文章中涉及的概念较多，但是感觉都没有很好的解释清楚，同时概念间的关联也不清晰。
    
    问题：
        
        1. 浏览器主线程（main thread）的事件驱动模型都做了什么？目前需要一个更为深入的心智模型来解释fiber架构 **** 参考[浏览器的一帧](https://wchfish.github.io/2023/07/08/frame-in-browser/)
        
        2. 什么是浏览器的刷新频率，以及每一帧（frame）中浏览器都做了什么？**** 参考[浏览器的一帧](https://wchfish.github.io/2023/07/08/frame-in-browser/)
* [React Fiber原理解析](https://juejin.cn/post/6844904202267787277)
    
    内容：对Fiber的作用和实现解释的不清楚
* [一篇长文帮你彻底搞懂React的调度机制原理](https://segmentfault.com/a/1190000039101758) ： 主要讨论了react中的task schedule
    
    内容：
        
        1. 介绍schedule，包括多个任务的管理（任务队列管理）和单个任务的执行控制（单个任务的中断和恢复），以及由此产生的“任务优先级”和“时间片”。
        
        2. 任务队列包括TaskQueue和TimerQueue，TimerQueue task到期 -> TaskQueue；task执行时间过长会中断。

        3. schedule的实现：任务概念，优先级概念；TimerQueue和TaskQueue是基于时间的优先队列（小顶堆）；任务中断与恢复的实现；任务取消的实现；
    
    问题：
        
        1. 任务队列、任务这些概念，以及中断等行为没有和react、宿主环境关联，所以术语显得很虚。
        2. react的操作（setState, useState等）到task的映射方式是什么？
* [浏览器的一帧](https://wchfish.github.io/2023/07/08/frame-in-browser/)
