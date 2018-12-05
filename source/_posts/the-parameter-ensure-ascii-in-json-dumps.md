---
title: json.dumps() 中的 ensure_ascii 参数
date: 2018-11-30 10:08:37
tags:
  - Python
---

在使用 `json.dumps()` 的时候，如果数据中包含中文，需要指定一个参数 `ensure_ascii` 的值为 `False`。

这是因为 `json.dumps()` 在序列化时，对中文默认使用 ASCII 编码。

```python
import json

print(json.dumps("中"))
# "\u4e2d"

print(json.dumps("中", ensure_ascii=False))
# "中"
```
