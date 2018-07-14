---
layout: post
title:  "Webserver开发日记-版本8"
date:   2018-07-14 14:32:00 +0800
categories: development-diary
tags: development-diary c++ epoll threadpoll
author: wwq
---

* content
{:toc}

Webserver开发日志（版本8）
====

修改部分
----
* 参考muduo，用双缓冲技术实现了log日志
* 重构thread有关代码

### ** Log实现逻辑: **
#### 首先是Logger类，Logger类里面有Impl类，其实具体实现是Impl类，我也不懂muduo为何要再封装一层，那么我们来说说Impl干了什么，在初始化的时候Impl会把
时间信息存到LogStream的缓冲区里，在我们实际用Log的时候，实际写入的缓冲区也是LogStream，在析构的时候Impl会把当前文件和行数等信息写入到LogStream，再
把LogStream里的内容写到AsyncLogging的缓冲区中，当然这时候我们要先开启一个后端线程用于把缓冲区的信息写到文件里.
#### 然后来说说LogStream类，里面其实就一个Buffer缓冲区，是用来暂时存放我们写入的信息的.还有就是重载运算符，因为我们采用的是C++ Stream的风格
#### 再来说说AsyncLogging类，这个是最核心的部分，我们知道在多线程程序中写Log无非就是前端往后端写，后端往硬盘写，首先前面提到了将LogStream的内容写>到了AsyncLogging缓冲区里，也就是前端往后端写，这个过程通过append函数实现，后端实现通过threadfunc函数，两个线程的同步和等待通过互斥锁和条件变量来实
现，具体实现使用了双缓冲技术，双缓冲技术的基本思路:准备两块buffer，A和B,前端往A写数据，后端从B里面往硬盘写数据，当A写满后，交换A和B，如此反复．不>过实际的实现的话和这个还是有点区别，具体看代码吧
#### 剩下的LogFile类和FileUtil类其实没什么好说的，就是把文件用RAII机制封装了，LogFile在FileUtil的基础上再封装增加了点功能罢了．

####这几天忙着投简历，都没什么空看muduo的源码了，花了挺多时间，终于让我读懂了log大概的流程，虽然还有一些小细节部分不是很懂，有空再多看几遍吧．希望自己能找到好工作
