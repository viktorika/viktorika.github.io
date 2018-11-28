---
layout: post
title:  "Webserver开发日记-版本10"
date:   2018-11-28 14:38:00 +0800
categories: development-diary
tags: development-diary c++ epoll threadpoll
author: wwq
---

* content
{:toc}

Webserver开发日志（版本10）
====

修改
----
* 修复了遇到sigpipe信号服务器崩溃问题
* 进一步优化Timer计时器结构
