
---
layout:     post
title:      Android taskAffinity
subtitle:   taskAffinity 和 launchmode
date:       2018-09-01
author:     mingshu
catalog: true
tags:
    - taskAffinity
---
# taskAffinity 的作用
taskAffinity：每个activity都有Affinity属性，该属性指出了它希望进入的栈，如果activity没有显示指明，该属性为application指定的affinity，如果application也没有指定，默认task为包名。
allowTaskReparenting属性：它进入后台，当一个和它有相同affinity的Task进入前台时，它会重新宿主，进入到该前台的task中。 
FLAG_ACTIVITY_NEW_TASK：

1. 当lauchMode 为standard, 指定 affinity 为其他栈 也不会启动新的task
1. 当lauchMode  为singleInstance, 指定 同一个affinity 也会启动新的task

# singleInstance 
1. 以singleInstance模式启动的Activity具有全局唯一性，即整个系统中只会存在一个这样的实例
2. 以singleInstance模式启动的Activity具有独占性，即它会独自占用一个任务，被他开启的任何activity都会运行在其他任务中（官方文档上的描述为，singleInstance模式的Activity不允许其他Activity和它共存在一个任务中）
3. 被singleInstance模式的Activity开启的其他activity，能够开启一个新任务，但不一定开启新的任务，也可能在已有的一个任务中开启
> https://www.cnblogs.com/wjw334/p/4789545.html 验证了以上三个性质