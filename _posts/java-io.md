也就是说一个完整的IO读请求操作包括两个阶段：
1. 查看数据是否就绪；

2. 进行数据拷贝（内核将数据拷贝到用户线程）。

# 阻塞IO- 非阻塞IO
那么阻塞（blocking IO）和非阻塞（non-blocking IO）的区别就在于第一个阶段，如果数据没有就绪，在查看数据是否就绪的过程中是一直等待，还是直接返回一个标志信息。

# 同步IO- 异步IO
同步IO： 当用户发出IO请求操作之后，如果数据没有就绪，需要通过用户线程或者内核不断地去轮询数据是否就绪，当数据就绪时，再将数据从内核拷贝到用户线程；
异步IO：只有IO请求操作的发出是由用户线程来进行的，IO操作的两个阶段都是由内核自动完成，然后发送通知告知用户线程IO操作已经完成。也就是说在异步IO中，不会对用户线程产生任何阻塞。
两者区别：同步IO和异步IO的关键区别反映在数据拷贝阶段是由用户线程完成还是内核完成。所以说异步IO必须要有操作系统的底层支持。
# 常见IO 模型
阻塞IO、非阻塞IO、多路复用IO、信号驱动IO以及异步IO。