---
title: Selenium 使用 Firefox 无头浏览器
date: 2017-03-04 12:08:59
tags:
  - Firefox
  - PhantomJS
  - Python
  - Selenium
---

目前 Selenium 已经停止对 PhantomJS 的支持。虽然 `webdriver.PhantomJS()` 仍然可以使用，但最佳选择应该是 Firefox 或者 Chrome 对应的无头浏览器，如果需要使用 Firefox 无头浏览器，可以按照以下方式开启：

```python
from selenium import webdriver
from selenium.webdriver.firefox.options import Options

options = Options()
options.add_argument("-headless")
driver = Firefox(firefox_options=options)
```

此时建立的 `webdriver` 对象就是一个 Firefox 的无头浏览器，如果需要使用 Chrome 无头浏览器，建立方法与 Firefox 差异不大。与 PhantomJS 无头浏览器相比，Firefox 无头浏览器建立对象的速度比较慢。
