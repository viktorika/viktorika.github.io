---
layout: post
title:  "Webserver开发日记-版本5"
date:   2018-07-04 20:53:00 +0800
categories: development-diary
tags: development-diary c++ epoll threadpoll 
author: wwq
---

* content
{:toc}

Webserver开发日志（版本5）
====

增加功能
----
* 支持命令行选项，-n为线程数目，-p为端口号，这里注意，我是主线程accept，其他线程处理读写操作的，所以必定有一个主线程，故-n 3表示1个主线程，3个副线程.
* 参照UNIX网络编程，用tcp_listen代替了socket,bind,listen过程，支持IPV6.

下一次的更新:打算重构HTTP解析模块
----
