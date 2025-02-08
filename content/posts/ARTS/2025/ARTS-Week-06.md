+++
title = 'ARTS Week 06, 2025'
date = 2025-02-05T09:56:28+08:00
categories = ['ARTS']
tags = ["AGI", "LLM"]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

[78. 子集 - 力扣（LeetCode）](https://leetcode.cn/problems/subsets/description/)

二进制枚举，时间复杂度$O(n * 2^n)$，空间复杂度$O(1)$。

创建一个0/1数列，长度为nums的长度，然后枚举这个数列的每个元素，如果为1，则将nums的元素加入到结果中。这一技巧叫做 **Gosper's Hack**。

| 0/1 序列 | 子集 | 0/1 序列对应的二进制数 |
| -------- | ---- | --------------------- |
| 000      | {}   | 0                     |
| 001      | {9}  | 1                     |
| 010      | {2}  | 2                     |
| 011      | {2,9}  | 3                     |
| 100      | {5}  | 4                     |
| 101      | {5,9}  | 5                     |
| 110      | {5,2}  | 6                     |
| 111      | {5,2,9}  | 7                     |

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        result = []
        n = len(nums)
        for i in range(1 << n):
            subset = []
            for j, x in enumerate(nums):
                if i >> j & 1:
                    subset.append(x)
            result.append(subset)
        return result
```

参考：[分享｜从集合论到位运算，常见位运算技巧分类总结！ - 力扣（LeetCode）](https://leetcode.cn/circle/discuss/CaOJ45/)



```python
sub = s
while True:
    # 处理 sub 的逻辑
    sub = (sub - 1) & s
    if sub == s:
        break
```

---

## 2.Review

[Docker executor | GitLab](https://docs.gitlab.com/runner/executors/docker.html#define-images-and-services-in-gitlab-ciyml)

1. 当使用`dind`服务的时候，必须使用tcp连接，而非sock连接。
2. 当使用[Kubernetes executor](https://docs.gitlab.com/runner/executors/kubernetes/index.html#using-dockerdind)时，会遇到Docker daemon还没启动，就尝试连接情况。

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

[Cannot connect to the Docker daemon]({{< ref "Cannot_connect_to_the_Docker_daemon" >}})
