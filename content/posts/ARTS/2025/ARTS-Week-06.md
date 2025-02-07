+++
title = 'ARTS Week 06, 2025'
date = 2025-02-05T09:56:28+08:00
categories = ['ARTS']
tags = ["AGI", "LLM"]
author=  "Abner Zhou"
draft = true
+++
## 1.Algorithm

[90. 子集 II - 力扣（LeetCode）](https://leetcode.cn/problems/subsets-ii/description/)



---

## 2.Review



---

## 3.Tip

Ubuntu Jammy 22.04 `netplan apply` 有一个bug，会报如下错误. [Bug #2041727](https://bugs.launchpad.net/ubuntu/+source/netplan.io/+bug/2041727)

```bash
bfinley@flashmq2:~$ sudo netplan apply
WARNING:root:Cannot call Open vSwitch: ovsdb-server.service is not running.
```

如果不在ubuntu中使用网络虚拟化、kvm之类的，这个bug不影响使用。如果要去掉报错，可以安装一下`openvswitch-switch`。

```bash
apt install openvswitch-switch
```

---

## 4.Share

[Minikube入门]({{< ref "Minikube入门" >}}): 快速启动一个Minikube集群

[Markdown添加参考文献]({{< ref "Markdown添加参考文献" >}})

[Kubernetes开发环境的选择]({{< ref "Kubernetes开发环境的选择" >}})