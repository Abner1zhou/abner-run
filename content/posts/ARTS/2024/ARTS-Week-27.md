+++
title = 'ARTS Week 27, 2024'
date = 2024-07-04T10:36:36+08:00
categories = ['ARTS']
tags = ["PostgreSQL", "dbt"]
author=  "Abner Zhou"
draft = false

+++
## 1.Algorithm

[283. 移动零](https://leetcode.cn/problems/move-zeroes/)

如果该位置为0，则pop该位置的元素 append到最后。

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        offset = 0
        for i in range(len(nums)):
            i = i - offset
            if nums[i] == 0:
                offset += 1
                nums.append(nums.pop(i))
```

---

## 2.Review

[How we structure our dbt projects](https://docs.getdbt.com/best-practices/how-we-structure/1-guide-overview)

dbt model可以分为3层，分别是staging、intermediate、

staging：主要负责从数据源中读取数据，并做一些简单的处理，比如重命名、格式转换等。

intermediate：处理数据的中间层，我们会讲staging中的数据做一些拼接、过滤、转换等。

marts：最终呈现给用户的数据，我们可以还在这一层根据业务需要来做聚合等。

---

## 3.Tip

no Tip this week

---

## 4.Share

[Postgresql_backup](https://abner.run/posts/postgresql_backup/)
