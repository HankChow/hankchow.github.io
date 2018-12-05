---
title: Python 在字典中根据条件筛选数据
date: 2018-12-01 14:26:51
tags:
  - Python
  - 奇技淫巧
---

首先创建一个字典

```python
import random

d = {str(x): random.randint(60, 100) for x in range(1, 21)}
print(d)
```

执行结果为

```python
{'1': 65, '2': 75, '3': 96, '4': 85, '5': 78, '6': 94, '7': 92, '8': 68, '9': 94, '10': 72, '11': 97, '12': 65, '13': 64, '14': 72, '15': 88, '16': 93, '17': 75, '18': 61, '19': 83, '20': 71}
```

如果需要在字典中筛选出值大于 90 的 id(key) 都有哪些，有以下四种实现方式：

* 循环迭代

```python
dd = {}
for k in d:
    if d[k] > 90:
        dd[k] = d[k]
print(dd)
```

  结果为：

```python
{'3': 96, '6': 94, '7': 92, '9': 94, '11': 97, '16': 93}
```

* `filter()` 函数

```python
dd = list(filter(lambda x: d[x] > 90, d))
print(dd)
```

  结果为：

```python
['3', '6', '7', '9', '11', '16']
```

* 字典解析式

```python
dd = {k: v for k, v in d.items() if v > 90}
print(dd)
```

  结果为：

```python
{'3': 96, '6': 94, '7': 92, '9': 94, '11': 97, '16': 93}
```

* 生成器解析式

```python
dd = ({k: v} for k, v in d.items() if v > 90)
for i in dd:
    print(i)
```

  结果为：

```python
{'3': 96}
{'6': 94}
{'7': 92}
{'9': 94}
{'11': 97}
{'16': 93}
```

