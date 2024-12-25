+++
title = 'ARTS Week 51'
date = 2024-12-23T10:16:17+08:00
categories = ['ARTS']
tags = [""]
author=  "Abner Zhou"
draft = true
+++
## 1.Algorithm

---

## 2.Review

[Develop on a remote Docker host](https://code.visualstudio.com/remote/advancedcontainers/develop-remote-host) in VS Code

使用Docker进行开发，往往受制于本地PC的内存大小，如果16G内存，那么能启动的容器数量就非常有限了，更别提MAC的黄金内存了。

所以我们可以选择借助VS Code的Dev Container插件连接到服务器上进行开发。

需要注意的是Linux的ssh-agent只能同时存在一个进程，否则就会出错。

```bash
ps -ax | grep 'ssh-agent -s'
```

如果存在多个进程，那么需要kill掉多余的进程。

```bash
pkill -9 ssh-agent
```

或者使用

```bash
killall ssh-agent
```

---

## 3.Tip

为了每周记录ARTS方便，快速的查询这是本年的第几周，可以同问这个网址[Week Numbers for 2024](https://www.epochconverter.com/weeks/2024)。

All weeks are starting on Monday and ending on Sunday.

---

## 4.Share

TODO 占个坑，写一下最近对于大模型应用开发的一些思考。

基于书《大模型应用开发极简入门：基于GPT-4和ChatGPT》