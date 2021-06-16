# JMM

1. 什么是JMM
   
   JMM:JAVA Memory Model
2. 有什么用
   
   缓存一致性协议，用于定义数据读写的规则
   
   JMM定义了线程工作和主内存之间的抽象关系：线程之间的共享变量存储在主内存（Main Memory）中，每个
   程都有一个私有的本地内存（Local Memory）

