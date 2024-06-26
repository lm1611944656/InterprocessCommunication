# 第一章 基础知识

在进行正式学习之前需要明白几个知识点；

1. Linux进程间通讯是在单机上，基于同一个Linux内核的不同进程之间通讯。
   - 同一个用户空间的不同进程不能进行进程间通讯，只能通过内核完成。
   - 根据内核中的对象不同，又可以划分为不同进程的通讯方式

![](.\StudyNoteImg\Linux进程间通讯.png)



2. Linux网络编程是在不同主机上，基于不同内核，采样一个网络的进行进程间通讯。

![](.\StudyNoteImg\Linux网络编程.png)



# 第2章 Linux进程间通讯

## 2.1 用户空间和内核空闲

![img](E:\Hardware\Linux进程间通讯\InterprocessCommunication\StudyNoteImg\v2-93c7015c4ca8888277406aa248d4a3d9_1440w.webp)

上图中的储户是没法直接从金库中存钱获取取钱的，如果这么做了，那么就非法了。这里用户空间相当于储户，内核空间相当于银行职员，而硬盘相当于金库，也就是用户空间中的进程没法直接操作读写硬盘中的数据，我们需要通过内核空间来处理，这样对于这两个概念应该会容易理解些。

|   空间   |                             描述                             |
| :------: | :----------------------------------------------------------: |
| 用户空间 | 是非特权区域，在该区域执行的代码不能直接访问硬件设备，常规进程就在本区域执行，JVM就是常规进程，所以JVM进程驻守在用户空间 |
| 内核空间 | 是操作系统所在区域，有特别的权利:能与设备控制器通讯，控制着用户区域进程的运行状态等等，最重要的是，所有I/O都直接或间接的通过内核空间 |

## 2.2 通讯方式

内核中对象的不同，决定了不同的通讯方式

通讯方式：

- 管道通讯
  - 有名管道(文件系统中有名)
  - 无名管道
- 信号通讯
  - 信号通讯包括：信号的发送、信号的接受和信号的处理；
- IPC通讯
  - 共享内存，消息队列和信号灯

**以上三种通讯方式都是单机通讯(在一个内核上进行)**

**socket通讯也是进程间通讯(存在一个网络中的两个进程间通讯)(两个Linux内核)**

# 第3章 管道

## 3.1 无名管道

无名管道：在文件系统中没有文件节点

## 3.2 有名管道

有名管道：在文件系统中有文件节点
