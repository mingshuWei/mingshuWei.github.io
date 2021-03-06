---
layout:     post
title:      Android WatchDog
subtitle:   Watchdog 简介和原理 
date:       2017-10-30
author:     mingshu
catalog: true
tags:
    - Fwk
    - WatchDog
---

# WatchDog 简介
Android的SystemServer是一个非常复杂的进程，里面运行的服务超过五十种，是最可能出问题的进程，因此有必要对SystemServer中运行的各种线程实施监控。但是
如果使用硬件看门狗的工作方式，每个线程隔一段时间去喂狗，不但非常浪费CPU，而且会导致程序设计更加复杂。因此Android开发了WatchDog类作为软件看门狗来监
控SystemServer中的线程。一旦发现问题，WatchDog会杀死SystemServer进程。WatchDog功能主要是分析系统核心服务和重要线程是否处于Blocked状态。
Watchdog继承于Thread，创建的线程名为”watchdog”。mHandlerCheckers队列包括、 主线程，fg, ui, io, display线程的HandlerChecker对象。

# WatchDog 工作原理
有两种方式加入Watchdog监控：
- addThread()：用于监测Handler线程，默认超时时长为60s.这种超时往往是所对应的handler线程消息处理得慢；
- addMonitor(): 用于监控实现了Watchdog.Monitor接口的服务.这种超时可能是”android.fg”线程消息处理得慢，也可能是monitor迟迟拿不到锁；能够
被Watchdog监控的系统服务都实现了Watchdog.Monitor接口，并实现其中的monitor()方法。运行在android.fg线程。

当watchdog的主循环开始运行后，每隔30秒，都会依次调用所有HandlerChecker的scheduleCheckLocked()方法。对于foreground thread的HandlerChecker，
由于它的mMonitors不为空，需要它去锁各服务的monitor()来检查是否出现死锁，因此每个检测周期都要执行它。
对于其他的HandlerChecker，需要判断线程的Looper是否处于Idling，若为空就说明前一个消息已经执行完毕正在等下一个，消息循环肯定没阻塞，不用继续检测直
接跳过本轮。如果线程的消息循环不是Idling状态，说明服务的主线程正在处理某个消息，有阻塞的可能，就需要使用PostAtFrontOfQueue发出消息到消息队列，并记录
下当前系统时间，同时将mComplete置为false，标明已经发出一个消息正在等待处理。
    
```
public void scheduleCheckLocked() {  
    if (mMonitors.size() == 0 && mHandler.getLooper().getQueue().isPolling()) {  
        // If the target looper has recently been polling, then  
        // there is no reason to enqueue our checker on it since that  
        // is as good as it not being deadlocked.  This avoid having  
        // to do a context switch to check the thread.  Note that we  
        // only do this if mCheckReboot is false and we have no  
        // monitors, since those would need to be executed at this point.  
        mCompleted = true;  
        return;  
    }  

    if (!mCompleted) {  
        // we already have a check in flight, so no need  
        return;  
    }  

    mCompleted = false;  
    mCurrentMonitor = null;  
    mStartTime = SystemClock.uptimeMillis();  
    mHandler.postAtFrontOfQueue(this);  
}  
```

    
如果线程的消息队列没有阻塞，PostAtFrontOfQueue很快就会触发HandlerChecker的run方法。对于foreground thread的HandlerChecker，它会回调被监控
服务的monitor方法，对其关键区上锁并马上释放，以检查是否存在死锁或阻塞。对于其他线程，仅需要将mComplete标记为true，表明消息已经处理完成即可。
    
```
@Override  
public void run() {  
        final int size = mMonitors.size();  
        for (int i = 0 ; i < size ; i++) {  
            synchronized (Watchdog.this) {  
                mCurrentMonitor = mMonitors.get(i);  
            }  
            mCurrentMonitor.monitor();  
        }  

        synchronized (Watchdog.this) {  
            mCompleted = true;  
            mCurrentMonitor = null;  
        }  
    }  
} 
```


以上内从参考如下两片博文
1. Android7.0 Watchdog机制 [见此处](https://blog.csdn.net/fu_kevin0606/article/details/64479489)
2. Gityuan WatchDog机制讲解 [见此处](http://gityuan.com/2016/06/21/watchdog/)

# 扩展阅读
    待扩展……^_^
