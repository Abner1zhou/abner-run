+++
title = 'ARTS Week 26, 2024'
date = 2024-06-25T09:48:14+08:00
categories = ['ARTS']
tags = ["数据库", "WDL"]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

---

## 2.Review

[WDL 1.2.0: Enhancing Workflow Description Language for Bioinformatics](https://openwdl.org/wdl/bioinformatics/workflows/announcing-wdl-1-2-0/)

One of the key improvements in WDL 1.2.0 is the introduction of the `Directory`type. 支持将目录作为输入输出参数

```wdl
version 1.2

task directory_output {
    command <<<
    mkdir out
    for n in {1..10}; do
      echo $n > out/file.$n
    done
    >>>

    output {
        Directory dir = "out/"
    }
}
```

但是使用目录作为输入会有一些功能差异，比如S3的对象存储不能为目录提供`checksum`，意味着使用目录作为输入无法保证工作流的一致性，也就意味着job caching无法使用。

引入了两个新的段落 `requirements`和`hints`用来代替`runtime`。`runtim`用来描述任务运行所需的资源，比如内存、CPU，但是有两个问题：

- 它允许使用任意属性，但并非所有 WDL 执行引擎都支持这些属性。
- 它将`requirements`（任务运行必须具备的资源）和`hints`（执行引擎可用于优化任务执行）混合在一起，但并非严格要求的属性。

`requirements`里包含了任务的硬性资源要求，如果无法满足，人物就会失败。`hints`里包含了对于资源的期望，根据计算节点的资源来判断是否需要满足这一部分资源。

---

## 3.Tip

数据库自动备份脚本

```bash
#!/bin/bash

# MySQL登录信息
USER="your_mysql_user"
PASSWORD="your_mysql_password"
HOST="your_mysql_host"

# 数据库列表
DATABASES=("db1" "db2" "db3")

# 备份目录
BACKUP_DIR="/path/to/backup"

# 日期格式
DATE=$(date +'%Y-%m-%d')

# 保留备份天数
RETENTION_DAYS=7

# 创建备份目录
mkdir -p $BACKUP_DIR

# 备份每个数据库
for DB in "${DATABASES[@]}"; do
  mysqldump -u $USER -p$PASSWORD -h $HOST $DB > "$BACKUP_DIR/${DB}_$DATE.sql"
done

# 删除超过保留天数的备份
find $BACKUP_DIR -type f -name "*.sql" -mtime +$RETENTION_DAYS -exec rm {} \;

# 日志记录
echo "Backup completed on $DATE" >> "$BACKUP_DIR/backup.log"

```

---

## 4.Share
