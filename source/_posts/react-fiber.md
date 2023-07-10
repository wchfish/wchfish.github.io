---
title: react fiber 架构解析
---

## 相关概念
* MessageChannel
* Fiber Node，Fiber Tree：根据react element生成，Fiber Tree通过对current和workInProgress做diff，更新VDOM。
    
    1. Fiber Node除了包含节点自身的信息外，还有子节点、兄弟节点、父节点的指针；Fiber Tree是一个链表结构。 

    2. Fiber Tree的遍历基于DFS算法。

    2. current fiber tree是上一次commit的快照，WrokInProgress fiber tree是当前在进行的更新。
* schedule: react render等操作会生成task，由schedule负责调度。schedule的思想是控制事件循环中单次js调用的执行时间，保证浏览器每一帧在限制时间（16.6ms）内完成，这样就不会block用户交互以及其他高优先级的任务。
    
    1. task支持中断、恢复、终止。每个fiber节点是task执行时的最小单元(unit work)。
    
    2. 任务有TimerQueue和TaskQueue两个优先队列保存。TimeQueue sort key是startTime，TaskQueue sort key 是ExpirationTime。

    3. 任务有优先级，schedule会优先执行高优任务。
* react更新UI有2个阶段，render和commit。render是异步的，commit是同步的需要一次性完成。
* 浏览器刷新率，一帧：react schedule依赖的基础。

## 问题
* react中schedule对应的task的详细内容，如task是怎么生成的，任务的优先级怎样确定等，任务在执行阶段做了什么？
* react element、Fiber节点、VDOM节点之间的关系是什么？

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

        2. react的操作（setState, useState等）到task的映射方式是什么？浏览器事件处理到task的映射关系是什么？
* [React 任务调度](https://xie.infoq.cn/article/dae49299746f3f3181f31b396): 写的比较好，思路清晰，行文流畅

    内容：

        1. jsx -> Fiber Tree的示例，fiber节点以及fiber tree的结构。

        2. react15 stack vs react16 fiber的实际例子（没有说明示例做了什么），性能差异原因的简单分析。

        3. 浏览器中一帧的概念，react基于帧的时间分片概念。

        4. 任务调度：包括任务优先级，TimerQueue和TaskQueue；

        5. 任务调度的示例。
    
    问题：
        1. react中的时间分片概念详解，时间分片是如何提高UI渲染性能的？时间分片在减少阻塞的同时，是否可能导致单个任务的执行时间变长？由此会产生哪些负面影响？
        
        2. 有哪些典型的场景可以用于分析fiber的渲染流程？

        3. 文章中的示例没有说清楚示例code是怎样执行的，很难对示例进行分析。

        4. 当浏览器的一帧耗时小于16.6ms时（包括了IdleCallback的执行），是否会立即进入下一帧？盲猜会立即进入下一帧。

        5. 任务优先级与用户交互事件的具体映射关系是什么？
* [深入 React 源码揭开渲染更新流程的面纱](https://xie.infoq.cn/article/1bd419f5ce928fa12ab1d6a5c) ： 结合源码分析react渲染流程，文中源码较多，阅读时需要静下心思考。
    
    内容：
        1. React15版本的架构分层。

        2. React16版本的架构分层：Schedule, Reconciler, Renderer;

        3. 基于渲染流程（初始render、setState）的源码分析。

        4. Schedule、Reconciler、Renderer三层结构的源码分析。
* [浏览器的一帧](https://wchfish.github.io/2023/07/08/frame-in-browser/)
* [视频课程](https://xiaochen1024.com/series/60b1b600712e370039088e24/60b1b636712e370039088e25)
