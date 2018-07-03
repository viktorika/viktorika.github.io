---
layout: post
title:  "Webserver开发日记-版本3"
date:   2018-07-03 22:49:00 +0800
categories: development-diary
tags: development-diary c++ epoll threadpoll 
author: wwq
---

* content
{:toc}

Webserver开发日志（版本3）
====

增加部分
----
* 增加了Timer计时器，解决http长连接的问题．
* 修复了一些bug，例如浏览器访问时请求favicon.ico图片的问题．

### **Timer计时器的处理逻辑：**
#### Timer里有两个数据结构：unordered_map和priority_queue，优先队列存放者TimerNode节点，只要节点的时间到了，或者该节点对应的channel事件关闭了那么该节点就可以删除，同时unorder_map是fd映射TimerNode节点，此TimerNode节点为存储在优先队列里的时间最久TimerNode节点，这里要注意，一个channel对应多个TimerNode节点，当该channel的TimerNode节点全部从优先队列中弹出时，删除掉该事件．这是我想到的比较好的Timer的处理方案．
