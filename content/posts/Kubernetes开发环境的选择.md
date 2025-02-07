+++
title = 'Kubernetes开发环境的选择'
date = 2025-02-07T17:12:12+08:00
categories = ["运维"]
tags = ["Kubernetes"]
author=  "Abner Zhou"
draft = false
+++

当我们手上的资源有限的情况下，如果要进行Kubernetes开发，可以使用Minikube、kind、k3s来本地部署一个小规模Kubernetes环境。

## Minikube、kind、k3s对比

**[Minikube](https://minikube.sigs.k8s.io/docs/)** 广泛使用于单节点的Kubernetes集群，可以直接部署在个人电脑上，在Windows、Mac、Linux系统上都能运行。能够快速、简单的部署一个测试、开发环境。Minikube支持多种虚拟化场景的部署，VirtualBox、VMware等[^1] ，甚至也能够在容器中运行。它也可以自定义启停某些Kubernetes组件，根据环境需要，来调整配置，能够将本地环境与生产环境保持一致。这种灵活性对于调试和确保应用程序在部署前按预期运行至关重要。
可以参考[Minikube入门]({{< ref "Minikube入门" >}})

**[Kind](https://kind.sigs.k8s.io/)** 项目由[Kubernetes SIG](https://kind.sigs.k8s.io/)牵头[^2]。Kind其实就是“Kubernetes in Docker“的简写，很显然，它通过docker 容器来创建Kubernetes集群，并将container作为nodes。Kind对于特别适合测试Kubernetes，尤其是在CI/CD方面。如果都是在Podman中运行，Kind会更加稳定且高效，因为Kind对podman做了更加全面的支持，并且支持rootless模式运行。

![kind](https://raw.githubusercontent.com/Abner1zhou/img_static/master/2025/02/6373bfdb2f11af77ee3c19f0faf22109-202502071713013.png)

**[K3S](https://k3s.io/)** 由[Rancher Labs](https://www.rancher.com/)开发并主导，定义为一个轻量的Kubernetes集群，针对于IOT或者边缘算。它的安装包非常小，并且支持一行命令无脑安装。适合类似树莓派等低功耗设备的快速部署。k3s 替换了一些Kubernetes的原生组件，比如用SQLite代替了etcd。k3s 还衍生出了 **[k3d](https://k3d.io/stable/)** 的项目，将k3s用docker容器封装了起来，可以使用docker更快的部署k3s。

## Popularity

截止2025年1月

1. minikube: >29.9k stars on GitHub
2. kind: >13.8k stars on GitHub
3. k3s: >28.7k stars on GitHub
4. k3d: >5.6k stars on GitHub

## Performance[^2]

**运行环境**：

Intel Core i7 (8th Gen) with 16 GiB RAM, Ubuntu

软件版本：

- minikube: minikube version: v1.26.1
- kind: kind v0.17.0 go1.19.2 linux/amd64
- k3d: k3d version v5.4.1

**集群启动时间**：

使用默认配置启动一个集群的时间

- minikube (docker): 29,448s
- k3d: 15,576 s
- kind: 19,691 s

**集群销毁时间**：

测量一个集群关闭、删除的时间

- minik
- ube (docker): 2,616 s
- k3d: 0,700 s
- kind: 0,805 s

**资源占用率**：

- minikube with docker (CPUs=8, Memory=15681 MiB):  
    CPU: ~20% Memory Usage: ~680.8 MiB
- K3d (CPUs=8, Memory=15681 MiB):  
    CPU: ~20% Memory Usage: ~502 MiB
- kind (CPUs=8, Memory=15681 MiB):  
    CPU: ~20% Memory Usage: ~581 MiB

## 如何在 Minikube, Kind, or K3s 中选择合适的方案

- **Minikube**: 一个开箱即用的全功能的Kubernetes工具，可以快速获得和生产环境一直的开发环境。
- **Kind**: 适合需要快速部署、临时测试的场景下使用，得益于容器的特性，可以通过配置文件将环境一丝不差的部署在任何地方。
- **K3s**: 适合部署轻量级的Kubernetes集群，适合在IoT设备、边缘计算等场景下使用。当设备性能不足、资源限制苛刻场景下的首选方案。

## Related

[^1]: [Minikube vs. Kind vs. K3s](https://www.devzero.io/blog/minikube-vs-kind-vs-k3s)

[^2]: [Minikube vs. k3d vs. kind vs. Getdeck | BLUESHOE](https://www.blueshoe.io/blog/minikube-vs-k3d-vs-kind-vs-getdeck-beiboot/)


