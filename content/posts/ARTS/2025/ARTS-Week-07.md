+++
title = 'ARTS Week 07, 2025'
date = 2025-02-12T17:02:42+08:00
categories = ['ARTS']
tags = ["Ceph", "SQL"]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

[90. 子集 II - 力扣（LeetCode）](https://leetcode.cn/problems/subsets-ii/)

```python
class Solution(object):
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        n = len(nums)
        result = []
        for mask in range(1 << n):
            subset = []
            flag = True
            for i in range(n):
                if mask & (1 << i):
                    if i > 0 and not (mask & (1 << (i - 1))) and nums[i] == nums[i - 1]:
                        flag = False
                        break
                    subset.append(nums[i])
            if flag:
                result.append(subset)
        return result
```

---

## 2.Review

[Ceph.io — Ceph Object Storage Tiering Enhancements. Part One](https://ceph.com/en/news/blog/2025/rgw-tiering-enhancements-part1/)

在Squid版本汇总，用户可以检索到已经冷备的数据，可以通过临时恢复或者永久恢复的方式来访问这些数据

- 临时恢复，指定对象文件文件生命周期，生命周期结束以后自动删除

- 把对象文件恢复到它之前所在的位置，并刷新这个对象的老化周期

[Ceph.io — Ceph Object Storage Tiering Enhancements. Part Two](https://ceph.com/en/news/blog/2025/rgw-tiering-enhancements-part2/)

- 对于开发人员来说，将后端的存储类型全抽象为S3 API，不需要去关注数据存放在性能区还是冷备区。

---

## 3.Tip

通过递归查询，将部门层级关系转换为树状结构

```sql
with department_hierarchy as (
    with recursive dept_tree as (
        select 
            dept_id,
            name,
            case 
                when parent_id = '1' then dept_id 
                else parent_id 
            end as parent_id,
            chanjet_code,
            1 as level,
            ARRAY[name] as path
        from stg_dingtalk__departments
        where parent_id = '1'
        
        union all
        
        select 
            d.dept_id,
            d.name,
            d.parent_id,
            d.chanjet_code,
            t.level + 1,
            t.path || d.name
        from stg_dingtalk__departments d
        inner join dept_tree t on d.parent_id = t.dept_id
    )
    select 
        dept_id,
        name as dept_name,
        parent_id as level_1_org_id,
        chanjet_code,
        path[1] as level_1_org
    from dept_tree
)
select * from department_hierarchy
```

---

## 4.Share
