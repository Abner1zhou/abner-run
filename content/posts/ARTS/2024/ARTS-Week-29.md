+++
title = 'ARTS Week 29, 2024'
date = 2024-07-15T10:38:34+08:00
categories = ['ARTS']
tags = ["oss"]
author=  "Abner Zhou"
draft = true
+++
## 1.Algorithm

---

## 2.Review

[How an empty S3 bucket can make your AWS bill explode](https://medium.com/@maciej.pocwierz/how-an-empty-s3-bucket-can-make-your-aws-bill-explode-934a383cb8b1)

阅读之前的问题：

1. 为什么OSS bucket name泄露可能导致恶意刷流量？

    在aws s3上面，会按照请求的次数收费，哪怕不是上传下载文件，也会产生一定的费用
    >Standard S3 PUT requests are priced at just [$0.005 per 1,000 requests](https://aws.amazon.com/s3/pricing/)

    阿里云对于请求失败不会另外收费

    ![image-20240717102734727](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/07/093dd7ee38bda91dfe0371b1dde5d8fd-image-20240717102734727.png)

2. 如何防止被攻击

    - 不要暴露自己的bucket name，使用随机的name；

    - 限制账户的余额、欠费额度，可以及时止损；

    - 配置监控告警，流量异常的时候可以选择拦截部分IP甚至直接关停服务
    - 要严格控制访问权限
    - 读写权限管控
    - 防盗链设置
        - ![image-20240717104531208](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/07/b4e56005e3a06e4de80cca7ecbfe75b5-image-20240717104531208.png)
    - 目录权限按需分配

3. 网站中使用的oss url中包含bucket name，怎么避免暴露？

​   不要使用默认的url，使用自己的域名替换file url。但还是可以通过cname解析查询到原始的bucket name

---

## 3.Tip

分享安卓工具 [Swift Backup](https://swiftapps.org/)

---

## 4.Share

[Migrate RAID to new server](/posts/migrate_raid_to_new_server/)