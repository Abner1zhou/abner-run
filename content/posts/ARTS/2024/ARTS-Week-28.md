+++
title = 'ARTS Week 28, 2024'
date = 2024-07-13T21:09:57+08:00
categories = ['ARTS']
tags = [""]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

[LCR 159. 库存管理 III](https://leetcode.cn/problems/zui-xiao-de-kge-shu-lcof/)

### 方法一：排序

```python
class Solution:
    def inventoryManagement(self, stock: List[int], cnt: int) -> List[int]:
        stock = sorted(stock)
        return(stock[:cnt])
```

对原数组从小到大排序后取出前 cnt 个数即可。

### 方法二：堆

我们用一个大根堆实时维护数组的前 cnt 小值。首先将前 cnt 个数插入大根堆中，随后从第 cnt+1 个数开始遍历，如果当前遍历到的数比大根堆的堆顶的数要小，就把堆顶的数弹出，再插入当前遍历到的数。Python 语言中的堆为小根堆，因此我们要对数组中所有的数取其相反数，才能使用小根堆维护前 *c**n**t* 小值。

```python
class Solution:
    def inventoryManagement(self, stock: List[int], cnt: int) -> List[int]:
        if cnt == 0:
            return list()

        hp = [-x for x in stock[:cnt]]
        heapq.heapify(hp)
        for i in range(cnt, len(stock)):
            if -hp[0] > stock[i]:
                heapq.heappop(hp)
                heapq.heappush(hp, -stock[i])
        ans = [-x for x in hp]
        return ans
```

---

## 2.Review

[Shooting conspiracies trend on X as Musk endorses Trump](https://www.theverge.com/2024/7/13/24198049/trump-x-shooting-conspiracy-theories-trending)

可能改变历史的一枪

![IMG_1712](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/07/ee26e48ddd5b9c8bf50015ea9b27b3db-IMG_1712.jpg)

---

## 3.Tip

[CF-Workers-docker](https://github.com/Abner1zhou/CF-Workers-docker.io)

通过Cloudflare Worker搭建免费的docker hub加速器

---

## 4.Share
