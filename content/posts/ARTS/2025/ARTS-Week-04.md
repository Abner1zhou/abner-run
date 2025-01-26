+++
title = 'ARTS Week 04, 2025'
date = 2025-01-24T10:02:49+08:00
categories = ['ARTS']
tags = ["动态规划", "Docker"]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

[2944. 购买水果需要的最少金币数](https://leetcode.cn/problems/minimum-number-of-coins-for-fruits/)

**吐槽翻译！**原文是：If you purchase the `i`<sub>th</sub> fruit at `prices[i]` coins, you can get any number of the next `i` fruits for free.

翻译是：如果你花费 prices[i] 购买了第 i 个水果，你可以免费获得下标范围在 [i + 1, i + i] 的水果。

正确的理解应该是买了第 i 个水果，该水果往后数 i 个水果可以免费拿。

```Python3
class Solution:
    def minimumCoins(self, prices: List[int]) -> int:
        n = len(prices)
        @cache  # 缓存装饰器，避免重复计算 dfs 的结果（记忆化）
        def dfs(i: int) -> int:
            if i * 2 >= n:
                return prices[i - 1]  # i 从 1 开始
            return min(dfs(j) for j in range(i + 1, i * 2 + 2)) + prices[i - 1]
        return dfs(1)
```

---

## 2.Review

[What is the Resolute Desk?](https://www.whitehousehistory.org/questions/what-is-the-resolute-desk-and-where-did-it-come-from)

Resolute Desk是美国总统的办公桌，放在白宫的总统办公室（Oval Office）。它是由19世纪时英国皇家海军舰艇——坚定号经改造制作而成的。在1880年由维多利亚女王赠予当时的美国总统。

![Resolute Desk](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2025/01/fcf2097a662d8777b432d1554306d5ee-202501261715396.png)

---

## 3.Tip

[Reducing Docker Logs Size](https://linuxiac.com/reducing-docker-logs-file-size/)

docker容器运行过程中会产生大量的日志，如果不进行定期清理，可能占用大量的硬盘空间。

**Docker日志只有在容器删除并重启后才会被清空**

使用以下命令查看容器日志大小

```bash
du -sh /var/lib/docker/containers/<container-id>/<container-id>-json.log
```

**清理容器日志**：

可以使用`truncate`命令清空日志文件

```bash
truncate -s 0 /var/lib/docker/containers/d2e9228f92b66ac09fa35dcab36abba2eb4a7f46baa1d03b65d71ed8d42de977/d2e9228f92b66ac09fa35dcab36abba2eb4a7f46baa1d03b65d71ed8d42de977-json.log
```

**一键删除所有容器日志**：

**注意：请理解以下命令的后果再操作**

```bash
truncate -s 0 /var/lib/docker/containers/*/*-json.log
```

**设置容器日志大小限制**：

修改`/etc/docker/daemon.json`文件，添加以下内容：

```json
{
  "log-driver": "json-file",
  "log-opts": {"max-size": "10m", "max-file": "3"}
}
```

---

## 4.Share

[Linux Interview Questions](https://labex.io/interview-questions/linux)

Linux 面试题