+++
title = 'ARTS Week 05, 2025'
date = 2025-02-01T13:16:25+08:00
categories = ['ARTS']
tags = ["AGI", "LLM"]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

[33. 搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/)

**要求**：时间复杂度 O(logn)

**解题思路**：由于数组是升序排列，然后旋转了一次，那么数组经过二分法以后，一定有一半是有序的，如果target在有序的部分中，就对有序的部分进行二分查找，如果target不在有序的部分中，就对另一半进行二分查找。

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if not nums:
            return -1
        n = len(nums)
        l, r = 0, n - 1
        while l <= r:
            mid = (r + l) // 2
            if nums[mid] == target:
                return mid
            if nums[0] <= nums[mid]:
                if nums[0] <= target < nums[mid]:
                    r = mid - 1
                else:
                    l = mid + 1
            else:
                if nums[mid] < target <= nums[n-1]:
                    l = mid + 1
                else:
                    r = mid - 1
            
        return -1
```

升级版：[81. 搜索旋转排序数组 II](https://leetcode.cn/problems/search-in-rotated-sorted-array-ii/)

题目考察的是如何尽可能的减少时间复杂度，题目中给出的数组是旋转排序数组，所以可以考虑使用二分查找来减少时间复杂度。

**要求**：尽可能的减少时间复杂度

**解题思路**：这题最简单的解法就是变量，并且速度也不慢，但是题目要求尽可能的减少时间复杂度，所以需要考虑二分查找。

相对于33题，需要考虑数组中存在重复元素的情况。如果出现a[l]=a[mid]=a[r]，那么就无法判断target在哪一边，所以需要将l和r都加1，然后继续二分查找。

```python
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        if not nums:
            return False
        
        n = len(nums)
        if n == 1:
            return nums[0] == target
        l, r = 0, n - 1
        while l <= r:
            mid = (l + r) //2
            if nums[mid] == target:
                return True
            if nums[l] == nums[mid] and nums[mid] == nums[r]:
                l += 1
                r -= 1
            elif nums[l] <= nums[mid]:
                if nums[l] <= target and target < nums[mid]:
                    r = mid -1
                else:
                    l = mid + 1
            else:
                if nums[mid] < target and target <= nums [n-1]:
                    l = mid + 1
                else:
                    r = mid - 1
        return False
```

---

## 2.Review

[China’s DeepSeek AI is hitting Nvidia where it hurts | The Verge](https://www.theverge.com/2025/1/27/24352801/deepseek-ai-chatbot-chatgpt-ios-app-store)

DeepSeek用OpenAI 6%的开发成本，1/8的算力算力资源实现了ChatGPT O1模型相同的性能。

DeepSeek的发布也使投资者怀疑Nvidia的价值是否被高估，以及Startgate $500 billion的投资是否有必要。

---

## 3.Tip

[在Chrome中复制链接同时复制标题解决方案 - soarli博客](https://blog.soarli.top/archives/670.html)

在使用Edge的时候，可以很方便的复制标题+URL，但在Chrome或者Brave中一直没有找到这个设置的位置。 然后发现了[Tab Copy](https://chromewebstore.google.com/detail/tab-copy/micdllihgoppmejpecmkilggmaagfdmb)这个插件，可以直接将标题+URL复制成Markdown的格式。

![tab copy popup](/images/tabcopy.webp)

![tab copy menu](/images/tabcopy-menu.webp)


---

## 4.Share

[微服务的划分方式](/posts/微服务的划分方式/)

新的业务可以先从单体架构开始，然后逐步拆分成微服务。