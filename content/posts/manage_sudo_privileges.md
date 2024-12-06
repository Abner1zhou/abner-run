+++
title = '管理sudo权限'
date = 2024-12-06T16:33:52+08:00
categories = ["运维"]
tags = ["Linux"]
author=  "Abner Zhou"
draft = false
+++

## 把账号加到`sudo`组里面

### Debian/Ubuntu

运行以下命令，添加用户到`sudo`组中

```bash
sudo usermod -aG sudo username

# Verify the user is added to the `sudo` group
groups username
```

### RHEL/CentOS/Rocky Linux

把用户添加到`wheel`组当中

```bash
usermod -aG wheel username

# Verify the user is added to the `wheel` group:
groups username
```

### 检查权限

切换到这个用户下

```bash
sudo whoami
```

输出应该是`root`

## 指定权限

通过`visudo`来修改`sudo`用户的权限

### 只允许用户执行某一个命令

在配置文件中加入类似这样的一行

```bash
username ALL=(ALL) NOPASSWD: /usr/local/bin/manage_user.sh
```

### 授予全部权限

```bash
username ALL=(ALL) NOPASSWD: ALL
```

- `ALL=(ALL)`: 全部权限.
- 第三个`ALL`：全部命令
- `NOPASSWD`: 使用`sudo`的时候不需要密码

### **第一个 `ALL`** (主机)

第一部分的 `ALL` 表示用户可以从任何主机运行指定的命令。可以替换为特定的主机名或 IP 地址。

#### 示例

`username myserver=(ALL) ALL`

- `myserver`: 只允许用户在主机名为 `myserver` 的机器上使用 `sudo`。
- 如果是多主机环境，可以指定多个主机：
    `username host1,host2=(ALL) ALL`
- 支持使用网络地址：
    `username 192.168.1.0/24=(ALL) ALL`

比如可以限定用户只能通过堡垒机执行sudo

### 第二个`ALL`（目标用户）

**这里需要特别说明`sudo`的含义是`switch user do`**
> Another way to switch users or execute commands as others is to use the `sudo` command.

括号中的 `ALL` 表示用户可以以任何用户身份（包括 `root`）运行命令。可以替换为特定用户或用户组。

#### 示例

- **特定用户**：
    `username ALL=(root) ALL`
    只允许用户以 `root` 身份运行命令。
- **特定用户组**（以 `%` 开头表示组名）：
    `username ALL=(%admin) ALL`
    允许用户以 `admin` 组中的任何用户身份运行命令。
- **仅允许自己**：
    `username ALL=(username) ALL`
    只允许用户以自己的身份运行命令（无 `root` 权限）。

### 第二个`ALL`（命令列表）

**指定单个命令**：`username ALL=(ALL) /usr/bin/systemctl`
**指定多个命令**：`username ALL=(ALL) /usr/bin/systemctl, /usr/bin/journalctl`
**禁止命令**：
可以结合 `!` 来禁止某些命令：
`username ALL=(ALL) ALL, !/usr/bin/rm`
