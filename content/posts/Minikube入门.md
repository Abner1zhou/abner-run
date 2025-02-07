+++
title = 'Minikube入门'
date = 2025-02-07T17:02:03+08:00
categories = ["运维"]
tags = ["Docker", "Kubernetes"]
author=  "Abner Zhou"
draft = false
+++

## 安装minikube启动程序

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
sudo dpkg -i minikube_latest_amd64.deb
```

快速启动一个Kubernetes集群，使用Docker作为启动环境。不要使用root用户，新建一个用户，然后将其添加到docker group中。

```bash
minikube start --driver=docker
# To make docker the default driver
minikube config set driver docker
```

```bash
ubuntu@minikube:~$ minikube start --driver=docker
😄  minikube v1.35.0 on Ubuntu 22.04 (kvm/amd64)
✨  Using the docker driver based on user configuration
📌  Using Docker driver with root privileges
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.46 ...
💾  Downloading Kubernetes v1.32.0 preload ...
    > preloaded-images-k8s-v18-v1...:  333.57 MiB / 333.57 MiB  100.00% 454.41
    > gcr.io/k8s-minikube/kicbase...:  500.31 MiB / 500.31 MiB  100.00% 488.66
🔥  Creating docker container (CPUs=2, Memory=3900MB) ...
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: default-storageclass, storage-provisioner
💡  kubectl not found. If you need it, try: 'minikube kubectl -- get pods -A'
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```
带emoji的CLI，生动了很多🤣

如果没有安装kubectl，下面命令会自动安装它

```bash
minikube kubectl -- get pods -A
```

替换一下kubectl命令，方便操作。把它写入到`~/.bashrc`中，在会后面新增一行。

```bash
alias kubectl="minikube kubectl --"
```

启用dahboard

```bash
minikube dashboard
```
