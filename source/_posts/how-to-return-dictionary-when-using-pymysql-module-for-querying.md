---
title: 使用 pymysql 模块时查询返回字典的方法
date: 2018-11-30 10:10:14
tags:
  - MySQL
  - Python
  - 奇技淫巧
---

使用 `pymysql` 模块在 MySQL 中进行查询时，如果是使用以下这种默认的查询方法时，调用 `fetchone()` 和 `fetchall()` 返回的查询结果将会分别是元组和嵌套元组，只能使用下标去访问查询出来的每个字段的值，相当不方便，也不灵活。

```python
import pymysql

connection = {
    "host": "",
    "user": "",
    "passwd": "",
    "db": "",
    "charset": "utf8"
}

conn = pymysql.connect(**connection)
cursor = conn.cursor()
sql = "blabla"
cursor.execute(sql)
result = cursor.fetchall()
```

最方便的返回莫过于字典了，字段名作为键名，查询出来的值作为键值，与字段的顺序无关。需要在查询的时候返回字典，只需要在连接参数中指定一个 `cursorclass` 参数为 `pymysql.cursors.DictCursor` 即可，使用 `fetchone()` 和 `fetchall()` 返回的查询结果分别为字典和以每一行为一个字典组成的列表。

```python
import pymysql

connection = {
    "host": "",
    "user": "",
    "passwd": "",
    "db": "",
    "charset": "utf8",
    "cursorclass": pymysql.cursors.DictCursor
}
conn = pymysql.connect(**connection)
cursor = conn.cursor()
sql = "blabla"
cursor.execute(sql)
result = cursor.fetchall()
```
