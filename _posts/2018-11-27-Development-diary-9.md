---
layout: post
title:  "Webserver开发日记-版本9"
date:   2018-11-27 12:26:00 +0800
categories: development-diary
tags: development-diary c++ epoll threadpoll
author: wwq
---

* content
{:toc}

Webserver开发日志（版本9）
====

新增
----
* 使用eventfd进行线程通信，将fd分配工作视为io操作封装在Channel里加入epoll一起处理，便于管理
* 实现了自己的内存池，进一步优化性能 

内存池实现逻辑
----
* 参考STL的allocator分成16个内存池处理，每一个分别是8,16,24...的倍数，超过128的直接malloc，否则找到对应的处理逻辑处理，比如4就去8的池子处理，9就去16的池子处理，每个内存池的具体实现同https://github.com/cacay/MemoryPool，只不过改成了多线程的形式，具体的请去看下他的源码

~                                                                                                                                                                                                           
~                                                                                                                                                                                                           
~                                                                                                                                                                                                           
~                                                                                                                                                                                                           
~                                                           
