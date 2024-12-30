+++
title = 'ARTS Week 51'
date = 2024-12-23T10:16:17+08:00
categories = ['ARTS']
tags = [""]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

[3046. 分割数组](https://leetcode.cn/problems/split-the-array/description/)


```python
class Solution:
    def isPossibleToSplit(self, nums: List[int]) -> bool:
        nums1 = []
        nums2 = []
        nums = sorted(nums)
        for num in nums:
            if num not in nums1:
                nums1.append(num)
            elif num not in nums2:
                nums2.append(num)
            else:
                return False
        return True
        
```

```python
class Solution:
    def isPossibleToSplit(self, nums: List[int]) -> bool:
        return max(Counter(nums).values()) <= 2
```

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

1. 为了每周记录ARTS方便，快速的查询这是本年的第几周，可以同问这个网址[Week Numbers for 2024](https://www.epochconverter.com/weeks/2024)。

    All weeks are starting on Monday and ending on Sunday.

2. Debian12 静态路由设置

    ```text
    auto ens18
    iface ens18 inet dhcp

    auto ens19
    iface ens19 inet static
            address 10.0.114.48/24
            up ip route add 192.168.0.0/16 via 10.0.114.1
            down ip route del 192.168.0.0/16 via 10.0.114.1
            up ip route add 10.0.0.0/16 via 10.0.114.1
            down ip route del 10.0.0.0/16 via 10.0.114.1
    ```

    up 表示，接口up的时候创建这条路由

    down表示，接口down的是偶删除该路由

---

## 4.Share

TODO 占个坑，写一下最近对于大模型应用开发的一些思考。

基于书《大模型应用开发极简入门：基于GPT-4和ChatGPT》