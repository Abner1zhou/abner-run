+++
title = 'ARTS Week 21, 2024'
date = 2024-06-01T10:37:00+08:00
draft = false
tag
+++
## 1.Algorithm

[575. 分糖果](https://leetcode.cn/problems/distribute-candies/)

### 集合set

设糖果数量为 n，由于妹妹只能分到一半的糖果，所以答案不会超过 n/2，同时设这些糖果一共有 m 种，答案也不会超过 m。

```Python
class Solution:
    def distributeCandies(self, candyType: List[int]) -> int:
        n = len(candyType)
        m = len(set(candyType))
        if n / 2 < types:
            return int(n / 2)
        else:
            return int(m)
```

### 暴力法

生成代表糖果的给定 `nums`数组的所有排列，并确定所生成数组前半部分中唯一元素的数目。

*假设无法直接使用的 SET 的情况下使用*

### 优化的暴力法

女孩能得到的唯一糖果的最大数量可以是n/2，如果独特的糖果数量低于n/2的话，为了使女孩能得到的独特的糖果数量最大化，我们会将所有独特的糖果分配给女孩。因此，在这种情况下，女孩得到的独特糖果数量等于给定`candies`数组中的独特糖果总数。

### 排序

```java
public class Solution {
    public int distributeCandies(int[] candies) {
        Arrays.sort(candies);
        int count = 1;
        for (int i = 1; i < candies.length && count < candies.length / 2; i++)
            if (candies[i] > candies[i - 1])
                count++;
        return count;
    }
}
```

## 2.Review

## 3.Tip

## 4.Share
