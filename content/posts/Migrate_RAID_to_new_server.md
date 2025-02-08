+++
title = 'Migrate RAID to new server'
date = 2024-07-18T10:06:16+08:00
categories = ["DevOps"]
tags = ["Server"]
author=  "Abner Zhou"
draft = false
+++
## background

Server: Dell R730xd with H330 RAID Controller
Storage: 2x800G SSD configured in RAID 1
Requirement: Migrate the SSDs to a new server while maintaining the RAID 1 configuration and preserving data integrity

> 将SSD迁移至新的服务器，并保证RAID配置、数据不变

## Steps

To migrate RAID 1 configuration from the Dell R730xd with the H330 RAID controller to a new server, you can follow these steps:

> 从Dell R730xd服务器迁移RAID 1配置，可以按照以下的步骤进行

**Prepare the new server**: Ensure the new server has a compatible RAID controller

> 确保新服务器的RAID控制器适配，一般同一品牌的RAID控制器都能够适配

**Shut down the old server**: Power off the R730xd server containing the RAID 1 configuration.

> 关闭旧服务器

**Connect the disks to the new server**: Remove the two SSDs configured in the RAID 1 array from the old server. Install the two disks into the new server's RAID controller.

> 将两块硬盘插到新的服务器中，位置、顺序可以不一样。

**Import the foreign configuration**: When you power on the new server, the RAID controller will detect the existing RAID 1 configuration as a "foreign" configuration. You can then import this configuration into the new RAID controller.
You can do this through the PERC BIOS configuration utility by selecting "Import Foreign Configuration".

- Press `<F>` to automatically import the foreign configuration.
- Enter the BIOS Configuration Utility and navigate to the Foreign Configuration View.

> 新服务器开机，进入到RAID控制器中，会出现一个选择"Import Foreign Configuration"，导入外部配置，就可以将旧的RAID配置导入。

**Verify the RAID 1 configuration**: After importing the foreign configuration, ensure the RAID 1 array is properly recognized and functioning on the new server.

> 导入配置以后，确到RAID 1 阵列被正确的识别。到这一步，所有的工作就全部完成了！

---

## Refs

[Migrating virtual disks](https://www.dell.com/support/manuals/zh-cn/poweredge-rc-h830/perc9ugpublication/Migrating-virtual-disks?guid=guid-a49d952c-befe-4d48-9393-1d9f93e6c95e&lang=en-us)