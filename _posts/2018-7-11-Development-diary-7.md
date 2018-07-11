---
layout: post
title:  "Webserver开发日记-版本7"
date:   2018-07-11 10:14:00 +0800
categories: development-diary
tags: development-diary c++ epoll threadpoll
author: wwq
---

* content
{:toc}

Webserver开发日志（版本7）
====

修改部分
----
* 使用RAII机制封装锁，减少死锁可能性，让线程更安全
* 使用类似双缓冲的技术，子线程在执行主线程给的任务时，把emptyqueue置换给pendingfunctorqueue，之后对emptyqueue进行操作就可以了，这样可以减少临界区的代码，在主线程accept往子线程添加任务时反应更迅速

心得
----
前面几个版本基本上都是我上网查muduo的资料写的，到后来我实在是受不了了，一些论坛和技术博客说的不够透彻，我决定买一本<<Linux多线程服务端编程>>来看，现在只看到一部分，说实话我自己并不能完全消化这本书，估计只能以后某一部分思想用上了我再回头翻书．这次的版本更新主要是我看到了muduo里log异步日志实现那部分，他提到了双缓冲技术实现log，然后让我当初模块的某一部分也在纠结可能会阻塞长时间，但是我想不到方法解决，在我读到这里的时候我就想到了，可以用类似的技术搞定，不得不说此书很有用，没白买.
