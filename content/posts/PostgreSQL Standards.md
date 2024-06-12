+++
title = 'PostgreSQL开发规范'
date = 2024-06-12T10:01:10+08:00
draft = false
categories = ["运维"]
tags = ["数据库", "PostgreSQL"]
author=  "Abner Zhou"
+++

## 通用命名规则

【强制】对象名(表名、列名、函数名、视图名、序列名等)只能使用小写字母、下划线和数字,不能以数字开头,不能使用保留字[[1]](https://www.cnblogs.com/Thenext/p/15138404.html)

【强制】库名、表名限制命名长度,建议总长度不超过63个字符[\[1\]](https://www.cnblogs.com/Thenext/p/15138404.html)[\[2\]](https://developer.aliyun.com/article/60899)[\[3\]](http://www.postgres.cn/news/viewone/1/596)。

【强制】查询中的别名不能使用除小写字母、下划线和数字之外的其他字符,如中文[\[1\]](https://www.cnblogs.com/Thenext/p/15138404.html)。

## 表名命名规则

【推荐】表名使用复数形式[\[3\]](http://www.postgres.cn/news/viewone/1/596)。

【推荐】临时表以tmp_开头,子表以规则结尾,如分区表tbl,子表为tbl_2016等[\[1\]](https://www.cnblogs.com/Thenext/p/15138404.html)。

## 索引命名规则

【推荐】主键索引以pk_开头,唯一索引以uk_开头,普通索引以idx_开头[\[1\]](https://www.cnblogs.com/Thenext/p/15138404.html)。

## 库名命名规则

【推荐】库名最好与应用名称一致或便于识别[\[1\]](https://www.cnblogs.com/Thenext/p/15138404.html)[\[3\]](http://www.postgres.cn/news/viewone/1/596)。

【推荐】不建议使用public schema,应为每个应用分配对应的schema,schema名最好与用户名一致[\[1\]](https://www.cnblogs.com/Thenext/p/15138404.html)[\[3\]](http://www.postgres.cn/news/viewone/1/596)。

## 函数命名规则

【推荐】以select、insert、delete、update、upsert打头,表示操作类型

## 参考资料

\[1\][PostgreSQL 数据库开发规范——命名规范 & 设计规范](https://www.cnblogs.com/Thenext/p/15138404.html)

\[2\][PostgreSQL 数据库开发规范——阿里云开发者社区](https://developer.aliyun.com/article/60899)

\[3\][探探PostgreSQL开发规约](http://www.postgres.cn/news/viewone/1/596)
