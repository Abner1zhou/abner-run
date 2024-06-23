+++
title = 'ARTS Week 25, 2024'
date = 2024-06-23T16:20:04+08:00
draft = false
categories = ['ARTS']
tags = ['Docker', 'Frontend']
author=  "Abner Zhou"
+++
## 1.Algorithm

[520. 检测大写字母](https://leetcode.cn/problems/detect-capital/)

```python
class Solution:
    def detectCapitalUse(self, word: str) -> bool:
        if len(word) >= 2 and word[0].islower() and word[1].isupper():
            return False
        
        return all(word[i].islower() == word[1].islower() for i in range(2, len(word)))
```

## 2.Review

[Nobody wants to work with our best engineer](https://medium.com/atomic-engineer/i-fired-our-best-engineer-62112fea1e9f)

任何工作都需要团队协作，单兵作战的“特种兵”难以受到同事们的喜欢。

Jon said “If they can’t see the right way to go…” “You don’t need to be nice to be right…” 

不能一意孤行，接收别人的意见

## 3.Tip

RHEL 系发行版对应关系

- Fedora (根发行版-软件实时更新-只支持一年) >>某一版本作为基准版本 ⏬
- Centos Stream (长期稳定发行版-软件版本固定-RHEL 的测试版-支持 5 年) >> 进行稳定性测试后 ⏬
- Red Hat Enterprise Linux (红帽商业发行版-支持 5+5 年) >> 源码无修改二次编译 ⏬
- Rocky Linux （社区免费发行版-与 RHEL bug 级兼容-支持 5+5 年）
- PS：付费推荐 RHEL ，白嫖用 Rocky 。
- 示例：Fedora 34 > Centos Stream 9 > Red Hat Enterprise Linux 9 > Rocky Linux 9

## 4.Share

[vCenter通过修改主机配置文件来重置ESXi主机root密码](https://www.abner.run/posts/resetesxipassword/)
