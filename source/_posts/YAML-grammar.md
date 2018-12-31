---
title: YAML 语法
date: 2016-07-20 10:07:35
tags:
  - YAML
---

YMAL：YMAL Ain’t Markup Language

```yaml
---
# 一位职工记录
name: Example Developer
job: Developer
skill: Elite
employed: True
foods:
    - Apple
    - Orange
    - Strawberry
    - Mango
languages:
    ruby: Elite
    python: Elite
    dotnet: Lame
```


* YAML 总是以 --- （三个横杠）作为文件的开始，这是 YAML 格式的一部分；
* 普通的键值对直接以 key: value 的格式每行存储，冒号后面必须为一个空格；
* 对于列表，列表中的每个元素都以 - （一个横杠 + 一个空格）开始，且每个元素的缩进相同；
* 对于字典，字典中的每一个键值对和普通的键值对一样（其实整个文件存储的形式就是键值对），但同一个字典中每个键值对的缩进也要相同；
* 在值中含有冒号等引起解析歧义的字符时，需要用双引号将整个值包住；
* 使用 {{ var }} 来引用变量。
