+++
title = '聊一下Nas的数据安全'
date = 2024-09-10T09:56:37+08:00
categories = ["DevOps"]
tags = [""]
author=  "Abner Zhou"
draft = false

+++

我有一台旧电脑改造的Nas，安装的是UNRAID系统。最近在升级硬盘的时候，由于我的错误操作，导致数据丢失了一部分。我想借此事件来分享一下我对于Nas数据安全的一些看法。

## 事件复盘

我的nas里面原本是3块4T硬盘+1块2T硬盘，最近新收到了一块8T硬盘，想做一下升级。原本计划的是将2T硬盘拆下，换上8T硬盘，结果UNRAID要求最大的硬盘必须为校验盘。
