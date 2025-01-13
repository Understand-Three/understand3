---
title: 常用命令
---
MySQL 是一种流行的关系数据库管理系统，以下是一些常用的 MySQL 命令，用于执行各种数据库操作：

在命令行中使用时，需在语句末尾加分号 `;`
### 数据库操作

1. **启动 MySQL 服务**：
```sh
mysql.server start
```

2. **停止 MySQL 服务**：
```sh
mysql.server stop
```

3. **重启 MySQL 服务**：
```sh
mysql.server restart
```

4. **登录 MySQL**：
```sh
mysql -u username -p
```

输入密码后登录。

### 数据库管理
查看数据库
```sql
SHOW DATABASES
```

1. **创建数据库**：
```sql
CREATE DATABASE database_name;
```

2. **选择（使用）数据库**：
```sql
USE database_name;
```

3. **删除数据库**：
```sql
DROP DATABASE database_name;
```

### 表管理

1. **创建表**：
```sql
CREATE TABLE table_name (
 column1 datatype,
 column2 datatype,
 ...
);
```

2. **查看表结构**：
```sql
DESCRIBE table_name;
```

3. **删除表**：
```sql
DROP TABLE table_name;
```

4. **插入数据**：
```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
```

5. **查询数据**：
```sql
SELECT * FROM table_name WHERE condition;
```

6. **更新数据**：
```sql
UPDATE table_name SET column1 = value1 WHERE condition;
```

7. **删除数据**：
```sql
DELETE FROM table_name WHERE condition;
```

### 用户和权限管理

1. **创建用户**：
```sql
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
```

2. **授权**：
```sql
GRANT privileges ON database_name.* TO 'username'@'host';
```

3. **撤销权限**：
```sql
REVOKE privileges ON database_name.* FROM 'username'@'host';
```

4. **刷新权限**：
```sql
FLUSH PRIVILEGES;
```

5. **删除用户**：
```sql
DROP USER 'username'@'host';
```

### 数据备份和恢复

1. **备份数据库**（使用 `mysqldump`）：
```sh
mysqldump -u username -p database_name > backup.sql
```

2. **恢复数据库**（使用 `mysql`）：
```sh
mysql -u username -p database_name < backup.sql
```

这些是 MySQL 中一些基本且常用的命令，涵盖了数据库的创建、管理、用户权限设置以及数据的增删改查等操作。对于更高级的操作和特定的用例，MySQL 提供了更多的命令和选项。
