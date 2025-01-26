+++
title = 'ARTS Week 04, 2025'
date = 2025-01-24T10:02:49+08:00
categories = ['ARTS']
tags = ["Dynamic Programming", "Docker"]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

[2944. Minimum Number of Coins for Fruits](https://leetcode.cn/problems/minimum-number-of-coins-for-fruits/)

```Python3
class Solution:
    def minimumCoins(self, prices: List[int]) -> int:
        n = len(prices)
        @cache  # Cache decorator to avoid duplicate calculations of dfs results (memoization)
        def dfs(i: int) -> int:
            if i * 2 >= n:
                return prices[i - 1]  # i starts from 1
            return min(dfs(j) for j in range(i + 1, i * 2 + 2)) + prices[i - 1]
        return dfs(1)
```

---

## 2.Review

[What is the Resolute Desk?](https://www.whitehousehistory.org/questions/what-is-the-resolute-desk-and-where-did-it-come-from)

Resolute Desk is the president's desk in the Oval Office of the White House. It is made from the "HMS Resolute", which was transformed in the 19th century. In 1880, Queen Victoria presented it to the then-president.

![Resolute Desk](/images/fcf2097a662d8777b432d1554306d5ee-202501261715396.webp)

---

## 3.Tip

[Reducing Docker Logs Size](https://linuxiac.com/reducing-docker-logs-file-size/)

Docker containers generate a large amount of logs during operation. If not cleaned regularly, they may occupy a large amount of disk space.

**Docker logs are cleared only when the container is deleted and restarted.**

Use the following command to view the size of the container logs:

```bash
du -sh /var/lib/docker/containers/<container-id>/<container-id>-json.log
```

**Clear container logs**：

You can use the `truncate` command to clear the log file:

```bash
truncate -s 0 /var/lib/docker/containers/d2e9228f92b66ac09fa35dcab36abba2eb4a7f46baa1d03b65d71ed8d42de977/d2e9228f92b66ac09fa35dcab36abba2eb4a7f46baa1d03b65d71ed8d42de977-json.log
```

**Delete all container logs**：

**Note: Please understand the consequences of the following commands before operating**

```bash
truncate -s 0 /var/lib/docker/containers/*/*-json.log
```

**Set log size limit for containers**：

Modify the `/etc/docker/daemon.json` file and add the following content:

```json
{
  "log-driver": "json-file",
  "log-opts": {"max-size": "10m", "max-file": "3"}
}
```

---

## 4.Share

[Linux Interview Questions](https://labex.io/interview-questions/linux)

Linux interview questions
