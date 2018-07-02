---
layout: post
title:  "Webserver开发日记-版本1"
date:   2018-06-25 11:26:00 +0800
categories: development-diary
tags: development-diary c++ epoll threadpoll 
author: wwq
---

* content
{:toc}

Webserver开发日志（版本1）
====

模块
----
* Server:绑定端口，监听并且采用epoll模式处理IO.
* Packet:写了需要的包裹函数.
* Mimetype:封装了mime类型
* Http_conn:解析http协议

待解决问题
----
* 有时候数据没有读完就解析的bug
* 内存占用太大的问题，后面考虑用智能指针等方案解决
* 没有充分利用多核资源，后面增加线程池处理
* 代码不够灵活，考虑用reactor模式重构.
