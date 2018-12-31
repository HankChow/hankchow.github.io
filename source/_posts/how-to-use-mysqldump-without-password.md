---
title: MySQL 5.6 无口令 dump
date: 2018-04-09 11:44:33
tags:
  - Linux
  - MySQL
---

为了提高安全性，MySQL 5.6 开始在 `mysql` 和 `mysqldump` 命令中明文输入口令时报 Warning: Using apassword on the command line interface can be insecure. 的警告。

在使用 shell 脚本来导出数据的时候，还是不要使用明文口令为妙。对于 MySQL 5.6+，可以在配置文件（CentOS 7 中为 `/etc/my.cnf`）中加入以下内容，再使用 `mysqldump` 就不需要使用口令了。

```
[mysqldump]
user={MySQL 用户名}
password={口令}
```
