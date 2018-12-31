---
title: Python 的新式类和经典类
date: 2015-08-19 11:50:09
tags:
  - Python
  - 类
---

在 Python 中声明一个类的时候，如果这个类继承 `object` 类，这个类就是新式类；如果这个类没有继承任何类，这个类就是经典类。

```python
# 声明一个新式类
class new_class(object)：
    pass

# 声明一个经典类
class classic_class(object):
    pass
```

Python 的新式类已经兼容经典类，而且新式类已经解决了经典类中关于多继承的缺陷，因此在 Python 中推荐使用新式类。

```python
class A:
    def foo(self):
        print('called A.foo()')

class B(A):
    pass

class C(A):
    def foo(self):
        print('called C.foo()')

class D(B, C):
    pass

if __name__ == '__main__':
    d = D()
    d.foo()
```

B、C 是 A 的子类，D 多继承了 B、C 两个类，其中 C 重写了 A 中的 `foo()` 方法。

如果 A 是经典类，当调用 D 的实例的 `foo()` 方法时，Python 会按照深度优先的方法去搜索 `foo()` ，路径是 B-A-C ，执行的是 A 中的 `foo()`；

如果 A 是新式类，当调用 D 的实例的 `foo()` 方法时，Python 会按照广度优先的方法去搜索 `foo()` ，路径是 B-C-A ，执行的是 C 中的 `foo()`。

因为 D 是直接继承 C 的，从逻辑上说，执行 C 中的 `foo()` 更加合理，因此新式类对多继承的处理更为合乎逻辑。

在 Python 3.x 中的新式类已经兼容了经典类，无论 A 是否继承 `object` 类， D 实例中的 `foo()` 都会执行 C 中的 `foo()`。但是在 Python 2.7 中这种差异仍然存在，因此还是推荐使用新式类，要继承 `object` 类。
