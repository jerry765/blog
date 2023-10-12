---
title: 计算机网络笔记
date: 2023-10-08 19:42
mdate: 2023-10-12 15:37:51
categories: GEE
tags:
- computer network
---

>  参考书籍：计算机网络——自顶向下方法（原书第 8 版）

##  第 1 章 计算机网络和因特网

端系统（end system）通过通信链路（communication link）和分组交换机（packet switch）的网络连接到一起。

端系统通过因特网服务提供商（Internet Service Provider，ISP）接入因特网。每一个 ISP 网络都是独立管理的。

- TCP（Transmission Control Protocol，传输控制协议）
- IP（Internet Protoc，网络协议）

分布式应用（distributed application）：涉及多个相互交换数据的端系统。

与因特网相连的端系统提供了一个套接字接口（socket interface），因特网套接字接口是一套发送程序必须遵循的规则集合。

为了完成一项工作，要求两个（或多个）通信实体运行相同的协议。
// TODO：附图计算机网络协议 P5

**向一个 Web 服务器发出请求（即在 Web 浏览器中键入一个 Web 网页的 URL）所发生的情况**：
首先，计算机向该 Web 服务器发送一条连接请求报文，并等待回答。该 Web 服务器最终能接收到连接请求报文，并返回一条连接响应报文。得知请求该 Web 文档正常后，计算机则在一条 GET 报文中发送该网页的名字，而该网页的名字要从这台 Web 服务器上取回。最后，Web 服务器向你的计算机返回该 Web 网页（文件）。

协议（protocol）定义了在两个或多个通信实体之间交换的报文的格式和顺序，以及报文的发送/接收或其他事件所采取的操作。

WiFi：基于 IEEE 802.11 技术的无线 LAN（局域网）接入

为了从源端系统向目的端系统发送一个报文（message），源将长报文划分为较小的数据块，称为分组（packet）。在源和目的地之间，每个分组都通过通信链路（communication link）和分组交换机（packet switch）传送，交换机主要有路由器（router）和链路层交换机（link-layer switch）两类。

存储转发传输（store-and-forward transmission）：交换机在开始向输出链路传输该分组的第一个比特之前，必须接受到整个分组。

分组交换机具有一个输出缓存【output buffer，也称为输出队列（output queue）】，缓存充满时将出现分组丢失（丢包）（packet loss），到达的分组或已经排队的分组之一将被丢弃。

转发表（forwarding table）用于将目的地址（或目的地址的一部分）映射为输出链路。

通过网络链路和交换机移动数据有两种基本方法：电路交换（circuit switching）和分组交换（packet switching）。
在电路

