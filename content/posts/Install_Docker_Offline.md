+++
title = '离线安装Docker'
date = 2024-09-09T16:17:41+08:00
categories = ["DevOps"]
tags = ["Linux", "Docker"]
author=  "Abner Zhou"
draft = false
+++
## 背景

有一台CentOS 7.3 的服务器需要安装Docker，但是服务器无法连接公网。

## 安装方式

### 下载Docker二进制文件

在本地电脑，或者可以联网的服务器中下载二进制包，然后通过scp或者U盘的方式传入到服务器中

[二进制包下载链接](https://download.docker.com/linux/static/stable/x86_64/)

[官方安装步骤](https://docs.docker.com/engine/install/binaries/#install-static-binaries)

### 解压文件

```bash
tar xzvf /path/to/FILE.tar.gz
```

将文件复制到`/usr/bin/`目录下

```bash
sudo cp docker/* /usr/bin/
```

### 将Docker添加到Service中

新建`/usr/lib/systemd/system/docker.service`文件  

```bash
vim /usr/lib/systemd/system/docker.service
```

写入以下内容

```text
[Unit]
Description=Docker Application Container Engine
Documentation=https://docs.docker.com
After=network-online.target firewalld.service
Wants=network-online.target
 
[Service]
Type=notify
ExecStart=/usr/bin/dockerd
ExecReload=/bin/kill -s HUP $MAINPID
LimitNOFILE=infinity
LimitNPROC=infinity
LimitCORE=infinity
TimeoutStartSec=0
Delegate=yes
KillMode=process
Restart=on-failure
StartLimitBurst=3
StartLimitInterval=60s
 
[Install]
WantedBy=multi-user.target
```

### 启动Docker

```bash
sudo systemctl daemon-reload
sudo systemctl start docker
```

### （可选项）直接运行Docker

也可以不添加service直接运行docker，启动Docker daemon

```bash
sudo dockerd &
```
