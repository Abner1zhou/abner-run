+++
title = 'ARTS Week 49'
date = 2024-12-06T14:31:57+08:00
categories = ['ARTS']
tags = [""]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

[999. 可以被一步捕获的棋子数](https://leetcode.cn/problems/available-captures-for-rook/description/)

根据题意模拟即可：

遍历棋盘确定白色车的下标，用 (st,ed) 表示。

模拟车移动的规则，朝四个基本方向移动，直到碰到卒或者白色象或者碰到棋盘边缘时停止，用 cnt 记录捕获到的卒的数量。

---

## 2.Review

[SQL best practices – don’t compare count(*) with 0](https://www.depesz.com/2024/12/01/sql-best-practices-dont-compare-count-with-0/)

举一个SQL的例子

```sql
SELECT u.* FROM users u
WHERE 0 = (SELECT COUNT(*) FROM addresses a WHERE a.user_id = u.id);
```

这个sql想要筛选出没有地址的用户。这个sql有什么问题吗？它确实能够达到我们的目的。

但是！当一个用户拥有成千上万的地址的时候，数据库会尽职的执行这个计算任务，然后返回一个计算结果，才能把这个用户从结果中剔除出去。这样问题就显露出来了，我们在这个过程中执行了大量的没有必要的计算。

那么应该如何改正？我们可以使用`EXISTS`方法

```sql
SELECT u.* FROM users u
WHERE NOT EXISTS (SELECT FROM addresses a WHERE a.user_id = u.id);
```

如果存在这个结果，那么它会立马返回结果，而不是遍历所有数据。

数据库的优化重点就在于这些细节，可能在业务量不大的时候性能差距不大。但是当业务量增长时候，这些不规范的sql就会像是定时炸弹，不知道在什么时候就影响了业务，并且难以排查。

---

## 3.Tip

目前大模型应用开发已经非常方便了。以阿里的通义千问为例，选择好对应的模型，输入提示词就可以创建一个简单的应用

![qwen_craete_app](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/12/d6d6ec5eb97099a233e40f7b5ee7a40d-d6d6ec5eb97099a233e40f7b5ee7a40d-image-20241206165107247.png)

发布以后就可以通过API直接调用，比如这个翻译任务，可以先用Python将html拆解成小段，然后输入给大模型来翻译，效果非常的好。

这也是第一次尝试使用大模型的api，对比chat的方式，api能够更加高效的执行重复性的任务。

---

## 4.Share

[管理sudo权限](/posts/manage_sudo_privileges/)，主要分享以下内容

1. 如何精细化的管理sudo权限
2. sudoers配置文件中的含义
