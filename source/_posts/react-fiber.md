---
title: react fiber 架构解析
---

## reference
* [前端工程师的自我修养：React Fiber 是如何实现更新过程可控的](https://www.infoq.cn/article/flex4gdzigdmjueq4orw)
    内容：对fiber的概念没有解释清楚，文章中涉及的概念较多，但是感觉都没有很好的解释清楚，同时概念间的关联也不清晰。
    
    问题：
        2. 浏览器主线程（main thread）的事件驱动模型都做了什么？目前需要一个更为深入的心智模型来解释fiber架构 **** 参考[浏览器的一帧](https://wchfish.github.io/2023/07/08/frame-in-browser/)
        3. 什么是浏览器的刷新频率，以及每一帧（frame）中浏览器都做了什么？**** 参考[浏览器的一帧](https://wchfish.github.io/2023/07/08/frame-in-browser/)
* [React Fiber原理解析](https://juejin.cn/post/6844904202267787277)
    内容：对Fiber的作用和实现解释的不清楚
* [浏览器的一帧](https://wchfish.github.io/2023/07/08/frame-in-browser/)