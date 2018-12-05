---
title: MySQL 引擎 MyISAM 和 InnoDB 的区别
date: 2018-11-29 13:53:33
tags:
  - MySQL
---

MySQL 5.5 开始 InnoDB 成为 MySQL 的默认引擎（之前是 MyISAM）。

1. MyISAM 不支持事务，InnoDB 支持事务。对于 InnoDB 每一条 SQL 语句都默认封装成事务自动提交，但会影响速度。所以最好把多条 SQL 语句放在 begin 和 commit 之间组成一个事务。
2. MyISAM 不支持外键，InnoDB 支持外键。如果一个 InnoDB 表包含外键，这个表转为 MyISAM 表的时候会失败。
3. MyISAM 是非聚集索引，数据文件是分离的，索引保存的是数据文件的指针，主键索引和辅助索引是独立的。InnoDB 是聚集索引，数据文件和索引绑定在一起，因此必须要有主键，且通过主键索引的效率很高。但辅助索引需要两次查询，先查询到主键，然后再通过主键查询到数据。
4. MyISAM 用一个变量保存了整个表的行数，执行 `SELECT COUNT(*)` 的时候直接读出该变量即可，速度很快。InnoDB 不保存表的具体行数，执行 `SELECT COUNT(*)` 的时候需要全表扫描。
5. MyISAM 支持全文索引，查询效率较高。InnoDB 不支持全文索引。
6. MyISAM 更强调性能，更适用于执行 SELECT 较多的情况。InnoDB 更适用于 INSERT 和 UPDATE 较多的情况。
7. MyISAM 在 DELETE 操作时会重新建立一个表，InnoDB 会一行一行地删除记录。
8. MyISAM 不支持行锁，只支持表锁。MyISAM 同一个表上的读锁和写锁是互斥的，MyISAM 并发读写时如果等待队列中同时有读和写请求，默认写请求的优先级高，但 MyISAM 的写操作性能较低，会导致进程阻塞。InnoDB 支持行锁。

