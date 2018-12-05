---
title: Windows 下 Python 字符编码异常解决方案
date: 2018-11-29 11:47:43
tags:
  - Windows
  - Python
  - 编码
---

在中文 Windows 系统中，文件的默认字符编码为 GBK，如果将一段编码为 UTF-8 的数据流在 Windows 下写入文件，就可能会解析失败并抛出 UnicodeEncodeError 异常。

解决方案是在打开要写入的文件时在 `encoding` 参数中指定数据流的编码，这样就能在先从数据流的编码转换为目的编码，然后写入文件。

```python
f = open('something.txt', 'w', encoding='utf-8')
```

对于一些编码不规范的文件，在读取是可能会遇到 UnicodeDecodeError 异常，因为在文件中有可能夹杂了一些非法编码的字符。这种情况下 `open()` 可以接受一个 `errors` 参数，来指定如果遇到编码错误时应该如何处理。这个参数有两个枚举值，分别是 `strict` 和 `ignore`，前者在遇到异常的时候直接抛出异常并退出，后者为直接忽略。

```python
f = open('something.txt', 'w', encoding='utf-8', errors='ignore')
```
