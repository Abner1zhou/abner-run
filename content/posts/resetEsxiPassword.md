+++
title = 'vCenter通过修改主机配置文件来重置ESXi主机root密码'
date = 2024-06-12T14:29:02+08:00
categories = ["运维"]
tags = ["VMware", "ESXi"]
author=  "Abner Zhou"
draft = false
+++

## 背景

管理员一般通过vCenter来管理ESXi主机，时间长了，ESXi主机的root密码忘记了，本文主要介绍在vCenter中通过修改主机配置文件来修改ESXI主机的root密码。

### （备注：不用重启ESXi主机，不影响ESXi主机上的虚拟机。）

本文以vCenter 6.7为例，其余版本大同小异，版本不同图标位置有些小变化，但是思路不变。

## 1、提取主机配置文件

选中要操作的主机，右键选择“主机配置文件”>>点击“提取主机配置文件”。为方便标识，更改一下名称，如修改root密码。（前提是要求vSphere许可为企业增强版，否则会提示许可证不支持。）

![提取主机配置文件](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/06/9e07cc09255bc255a6cbc2b36ec460a6-9e07cc09255bc255a6cbc2b36ec460a6-image-11.png)

## 2、在“主机配置文件”中找到提取的配置文件

选择“菜单”>>“策略和配置文件”

![策略和配置文件](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/06/59fd631fa43033e1b1cb31e39edf83de-image-7-20240612143421219.png)

## 3、编辑主机配置文件

选中配置文件，点击”选中配置文件，右击点击“取消所有的勾选项。依次选择“安全和服务” >>“安全设置” >>“安全”>>“用户配置”，然后勾选“root”。将密码策略修改成“**固定的密码配置**”，输入要修改的密码，然后点击“保存”。

![编辑主机配置文件](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/06/ff6d0a8793a41c6fd334c909c89756b0-image-8-20240612143429740.png)

## 4、依次选中要重置密码的主机， 右键选择“主机配置文件”>>点击“附加主机配置文件”

![附加主机配置文件](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/06/3da39fda4339bb793db2323cd003a1cb-image-10-20240612143434543.png)

## 5、修复主机配置文件

选择“菜单”>>“策略和配置文件”，在“主机配置文件”中找到提取的配置文件。 

![修复主机配置文件](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/06/9e07cc09255bc255a6cbc2b36ec460a6-image-11-20240612143437926.png)

取消勾选“自动重新引导需要修复的主机”，点击修复。等待任务执行完毕。

或者直接在主机菜单中操作

![image-20240612143733769](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/06/6233f1eb070386da38b0ab603b8d17da-image-20240612143733769.png)

## 6、验证

登录web client，输入账号和密码进行验证。
