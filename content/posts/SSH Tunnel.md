+++
title = 'SSH Tunnel 端口转发'
date = 2024-06-05
draft = false
categories = ["Linux"]
tags = ["运维"]
+++
# SSH Tunnel

出于安全考虑只能通过堡垒机SSH访问内网资源，无法直接访问内网的HTTP、数据库等服务

环境拓扑如下：

{{< mermaid >}}
flowchart TD
	我的电脑 --SSH--> 堡垒机
	堡垒机 --> 内网服务器["内网服务器\nHTTP(80)\nMySQL(3306)"]
	
{{< /mermaid >}}

需要实现的目标是我的电脑能够访问内网服务器的HTTP和MySQL

## 实现方式

```shell
ssh -f -N -L localhost:8080:192.168.100.2:80 user@10.0.0.1
```

### 命令解释：

localhost：我电脑的监控地址

8080：我电脑的监听端口， 这样就可以在浏览器里面输入`localhost:8080`来访问内网服务器

192.168.100.2：内网服务器IP

80：内网服务器HTTP对应的端口

user@10.0.0.1： 堡垒机对应的用户名、IP



### ssh options 解释

**-f**    Requests ssh to go to background just before command execution.   把SSH会话放到后台运行

**-N**  Do not execute a remote command.  This is useful for just forwarding ports.   不执行`/bin/bash`之类的shell

**-L**   [bind_address:]port:host:hostport   转发端口