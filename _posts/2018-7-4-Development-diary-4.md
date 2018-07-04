---
layout: post
title:  "Webserver开发日记-版本4"
date:   2018-07-04 17:11:00 +0800
categories: development-diary
tags: development-diary c++ epoll threadpoll 
author: wwq
---

* content
{:toc}

Webserver开发日志（版本4）
====

改动部分
----
* 增加了线程池模块，加大了服务器的并发性能，采用one loop per thread的机制，想参考muduo，无奈不太好理解，暂时写得比较简陋，有待以后改进．
* 优化部分代码，提高一点性能.

待解决问题
----
* http解析bug，之后将用状态模式解决http解析问题，虽然暂时本地测试没出现bug，但是理论上高并发的时候会出现bug.
* 可以改成linux命令格式运行，通过参数控制线程池数量和监听端口号，使用起来更方便.
* makefile的重构，由于对makefile的了解不够深入，写得比较基础，有待之后学习后修改得更客观.
