---
layout: post
title:  "Webserver开发日记-版本6"
date:   2018-07-05 15:50:00 +0800
categories: development-diary
tags: development-diary c++ epoll threadpoll
author: wwq
---

* content
{:toc}

Webserver开发日志（版本6）
====

修改部分
----
* 重构了http_conn，用状态机解决了http解析问题，修复了解析bug，而且写法用了function和bind自认为比较优雅，可以参考一下.
* 增加了http错误处理功能，暂时统一按400错误码返回.以后有待改进.

有待增加的功能
----
功能基本已经完善，还能再加的话就是log日志了．
