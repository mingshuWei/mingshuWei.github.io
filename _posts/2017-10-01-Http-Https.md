---
layout:     post
title:      HTTP HTTPS
subtitle:   HTTP PKI 加解密  
date:       2017-10-01
author:     mingshu
catalog: true
tags:
    - HTTP HTTPS
    - 对称加密 非对称加密
    - PKI 证书
---

# HTTP
1. 五层模型
应用层，传输层，网络层，链接层，实体层
实体层： 把电脑连接起来的物理手段。它主要规定了网络的一些电气特性，作用是负责传送0和1的电信号
链接层： 它在"实体层"的上方，确定了0和1的分组方式。以太网协议以太网规定，一组电信号构成一个数据包，叫做"帧"（Frame）。每一帧分成两个部分：标头（Head）和数据（Data）
网络层： 它的作用是引进一套新的地址，使得我们能够区分不同的计算机是否属于同一个子网络。这套地址就叫做"网络地址"，简称"网址"。
传输层： 建立"端口到端口"的通信。相比之下，"网络层"的功能是建立"主机到主机"的通信。只要确定主机和端口，我们就能实现程序之间的交流。因此，Unix系统就把主机+端口，叫做"套接字"（socket）
应用层： 就是规定应用程序的数据格式。
> 参考文章 阮一峰 http://www.ruanyifeng.com/blog/2012/05/internet_protocol_suite_part_i.html
> Http 详解 https://www.jianshu.com/p/80e25cb1d81a
# HTTPS
HTTPS (Secure Hypertext Transfer Protocol)安全超文本传输协议，是一个安全通信通道，它基于HTTP开发用于在客户计算机和服务器之间交换信息。它使用安全套接字层(SSL)进行信息交换，简单来说它是HTTP的安全版,是使用TLS/SSL加密的HTTP协议
1. 信息加密
2. 完整性校验
3. 身份验证
> HTTPS加密协议详解(一)：HTTPS基础知识 https://www.wosign.com/faq/faq2016-0309-01.htm
> HTTPS加密协议详解(二)：TLS/SSL工作原理 https://www.wosign.com/faq/faq2016-0309-02.htm
> HTTPS加密协议详解(三)：PKI 体系 https://www.wosign.com/faq/faq2016-0309-03.htm
> 图解SSL/TLS协议 RSA DH 正常的五步握手与DH握手的关系与区别 https://www.cnblogs.com/my_life/articles/5857614.html


Android安全开发之安全使用HTTPS https://www.cnblogs.com/alisecurity/p/5939336.html
HTTPS 原理浅析及其在 Android 中的使用 https://zhuanlan.zhihu.com/p/27040041?utm_medium=social&utm_source=weibo