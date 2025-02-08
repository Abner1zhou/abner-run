+++
title = 'Postgresql_backup'
date = 2024-07-13T21:26:10+08:00
categories = ["DevOps"]
tags = ["数据库", "PostgreSQL"]
author=  "Abner Zhou"
draft = false
+++

### 使用 `pg_dump` 进行逻辑备份

`pg_dump` 是 PostgreSQL 自带的工具，用于创建数据库的逻辑备份。它生成一个包含SQL语句的文件，可以用来重建数据库。

#### 示例脚本

```bash
#!/bin/bash

# PostgreSQL登录信息
USER="your_pg_user"
PASSWORD="your_pg_password"
HOST="your_pg_host"
PORT="5432"

# 数据库列表
DATABASES=("db1" "db2" "db3")

# 备份目录
BACKUP_DIR="/path/to/backup"

# 日期格式
DATE=$(date +'%Y-%m-%d')

# 保留备份天数
RETENTION_DAYS=7

# 设置PGPASSWORD环境变量
export PGPASSWORD=$PASSWORD

# 创建备份目录
mkdir -p $BACKUP_DIR

# 备份每个数据库
for DB in "${DATABASES[@]}"; do
  pg_dump -U $USER -h $HOST -p $PORT -F c -b -v -f "$BACKUP_DIR/${DB}_$DATE.backup" $DB
done

# 删除超过保留天数的备份
find $BACKUP_DIR -type f -name "*.backup" -mtime +$RETENTION_DAYS -exec rm {} \;

# 日志记录
echo "Backup completed on $DATE" >> "$BACKUP_DIR/backup.log"
```

### 2. 使用 `pg_basebackup` 进行物理备份

`pg_basebackup` 是用于备份整个数据库集群的物理备份工具，适用于流复制或备份大型数据库。

#### 示例脚本

```bash
#!/bin/bash

# PostgreSQL登录信息
USER="your_pg_user"
PASSWORD="your_pg_password"
HOST="your_pg_host"
PORT="5432"

# 备份目录
BACKUP_DIR="/path/to/backup"
DATE=$(date +'%Y-%m-%d')
BACKUP_PATH="$BACKUP_DIR/base_backup_$DATE"

# 设置PGPASSWORD环境变量
export PGPASSWORD=$PASSWORD

# 创建备份目录
mkdir -p $BACKUP_PATH

# 执行物理备份
pg_basebackup -U $USER -h $HOST -p $PORT -D $BACKUP_PATH -F t -z -P

# 删除超过保留天数的备份
find $BACKUP_DIR -type d -name "base_backup_*" -mtime +7 -exec rm -rf {} \;

# 日志记录
echo "Base backup completed on $DATE" >> "$BACKUP_DIR/backup.log"
```

### 备份验证和恢复测试

定期验证备份文件，并进行恢复测试以确保备份文件的有效性。如果是使用`pg_dump`进行的备份，可以使用 `pg_restore` 恢复逻辑备份：

```bash
pg_restore -U your_pg_user -h your_pg_host -d your_database -v "/path/to/backup/your_backup_file.backup"
```

如果使用`pg_basebackup`进行的物理备份，请市容如下命令恢复：

```bash
tar -xzf /path/to/backup/backup.tar.gz -C /path/to/postgresql/data
# 确保 PostgreSQL 服务已停止
pg_ctl -D /path/to/postgresql/data start

```

### `pg_dump` 和 `pg_basebackup`的对比

#### pg_dump

1. **类型**: 逻辑备份工具
2. **备份内容**: 数据库中的结构和数据（包括表、索引、视图、触发器等）。
3. **备份格式**: 可以生成SQL脚本或自定义格式文件。自定义格式（-Fc）可以用于增量备份和并行恢复。
4. **使用场景**: 适用于单个数据库的备份和恢复。尤其适用于小型数据库或需要备份到不同版本的 PostgreSQL 数据库时。
5. 优点：
   - 生成的SQL脚本可读，可编辑。
   - 支持部分恢复，可以选择性地恢复某些表或数据。
   - 跨版本兼容性较好。
6. 缺点：
   - 对于大型数据库，备份和恢复速度较慢。
   - 不包含WAL日志，不适用于物理复制和灾难恢复。

#### pg_basebackup

1. **类型**: 物理备份工具
2. **备份内容**: 整个数据库集群的物理文件（包括数据文件、配置文件、WAL日志等）。
3. **备份格式**: 生成整个数据库集群的目录或tar归档文件。
4. **使用场景**: 适用于大规模数据库的完整备份，灾难恢复，流复制和主从复制设置。
5. 优点：
   - 备份和恢复速度较快。
   - 包含WAL日志，适用于物理复制和灾难恢复。
   - 可以用于创建热备份，支持流复制。
6. 缺点：
   - 生成的备份不可读，不易编辑。
   - 只能备份整个数据库集群，不支持部分备份。
   - 只能恢复到相同版本的 PostgreSQL 实例。
