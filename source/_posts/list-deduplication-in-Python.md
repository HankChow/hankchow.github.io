---
title: Python 中的列表去重
date: 2018-11-29 12:01:38
tags:
  - Python
---

在 Python 中，普通列表可以使用 `set()` 来进行去重，这是使用了集合的唯一性，把列表转换为集合之后保证没有重复的元素，然后再使用 `list()` 把集合转换为列表。但这种方法并不保证元素之间的顺序，而且如果原列表之中含有不能被 hash 的元素（如字典、集合之类），原列表更无法转换为集合类型。

这种情况下应该保持列表的类型，使用 lambda 表达式进行去重：

```python
import functools.reduce
lst = [2, 3, 3, 1]
func = lambda x, y: x if y in x else x + [y]
functools.reduce(func, [[], ] + lst)
```

这个时候列表 lst 就是 [2, 3, 1] 了。
