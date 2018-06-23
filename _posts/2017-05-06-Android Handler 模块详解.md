---
layout:     post
title:      Android handler 模块详解
subtitle:   handler 实现机制 源码解析
date:       2017-05-06
author:     mingshu
catalog: true
tags:
    - Handler
    - Looper
    - Message
---



## Handler 简介

Android是消息驱动的，消息驱动包括Java层实现和Native层实现。Java层的消息机制包括Message、MessageQueue、Looper、Handler四要素， Native层的消息机制包括Looper、MessageQueue两要素。Handler是Android消息机制的统称，它主要是解决手机中进程内两个线程之间如何通讯。
消息驱动是围绕消息的产生与处理展开的，并依靠消息循环机制来实现。Hander 使用及简介[Handler API](https://developer.android.google.cn/reference/android/os/Handler)

> Note:如果你想了解 swift 3.0 中的新功能，可以看[这篇文章](https://www.raywenderlich.com/135655/whats-new-swift-3)。

## 深入详解 Handler Message Looper 之间的关系

android的消息处理有四个核心类：Looper,Handler和Message,MessageQueue（消息队列）, 个人理解 MessageQueue 就是一个容器，用来接受各个持有 handler 引用
的线程生产的 message。而 looper 所在的线程做为消费者，不断从容器 queue 中获取消费 message。

queue 是整个消息框架的核心实现机制，几个特点：
- queue 里面的消息是按照时间排序的
- queue 无消息可读则阻塞
- queue 读消息的时间小于头部消息的时间，则阻塞到message.when

looper:
- looper 是一个线程的动力，可以使一个线程不断的从queue 读取message，内部依靠for 循坏从queue 读取消息
- 也可以手动使用handler 结合 thread ，实现一个自己的后台线程，参考HandlerThead 的具体实现原理

> Note: [此篇文章](https://my.oschina.net/fireant/blog/264991) 图文并茂讲述了handler，message，looper之间的关系。

## 源码解读

源码部分主要从 Android 源码的实现讲解系统如何实现 handler 的机制，此部分可参考 gityuan 的文章。文章主要从两部分讲解 java 层和 native层。
- [消息机制 -java层](http://gityuan.com/2015/12/26/handler-message-framework/)
- [消息机制 -native 层](http://gityuan.com/2015/12/27/handler-message-native/)

## 扩张阅读

使用handler的都知道，我们可以使用handler post 延时消息。比如如下场景，先postDelay 一个100s延时，然后再postDelay 一个10s的延时，系统此时
是如何实现精确延时的。[此篇文章](http://www.dss886.com/2016/08/16/01/) 揭开了handler 如何实现精确延时的神秘面纱。其实java 中Timer的
精确延时也是这样。
## 结语


