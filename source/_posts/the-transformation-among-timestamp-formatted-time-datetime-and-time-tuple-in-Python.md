---
title: Python 中时间戳、格式化时间、时间数组、datetime 之间的转换
date: 2018-11-29 10:12:33
tags: 
  - Python
---

```python
import time
from datetime import datetime
 
# 获得时间戳
timestamp = time.time()
 
# 时间戳转为时间数组
time_array = time.localtime(timestamp)
 
# 时间数组转为时间戳
timestamp = time.mktime(time_array())
 
# 格式化时间转为时间数组
time_array = time.strptime(format_time, '%Y-%m-%d %H:%M:%S')
 
# 时间数组转为格式化时间
format_time = time.strftime('%Y-%m-%d %H:%M:%S', time_array)
 
# datetime 转为时间戳
ts = dt.timestamp()
 
# 时间戳转为 datetime
dt = datetime.fromtimestamp(ts)
 
# 直接输出当前的格式化时间
time.strftime('%Y-%m-%d %H:%M:%S')
```
