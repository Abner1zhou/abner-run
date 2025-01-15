+++
title = 'ARTS Week 03, 2025'
date = 2025-01-15T14:52:27+08:00
categories = ['ARTS']
tags = [""]
author=  "Abner Zhou"
draft = true
+++
## 1.Algorithm

---

## 2.Review

[Bare-metal k3s + Proxmox + 24TB CephFS](https://medium.com/@jakenesler/bare-metal-k3s-proxmox-24tb-cephfs-fc8e624bd7fe)

Proxmox是非常方便的超融合管理工具，操作系统使用的是Debian也容易维护，并且Proxmox内置了Ceph的安装程序，可以方便的创建出CephFS的存储集群。

自建本地的垃圾佬云集群，确实要比公有云成本低很多。 假设每台功率100W，24小时运行，每度电0.6元，那么一年的电费就是：

```
0.1kWh * 24h * 365d * 0.6元/度 * 3台 = 1576.8元
```

可以说是相当便宜了，这个成本在阿里云上面只能租一台2核2G的服务器，还不包括硬盘和带宽的费用。只要前期投入4-5000元，就可以搭建一个相当不错的集群了。对于独立开发者、或者小团队来说，可以节省不少成本。

---

## 3.Tip

通过[硬盘SMART参数](https://vanxkr.com/2024/11/SMART/)查看硬盘的健康状态。

---

## 4.Share
