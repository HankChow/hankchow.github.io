---
title: 为远程主机设置别名
date: 2015-03-01 11:38:55
tags:
  - Linux
  - ssh
---

在进行 `ssh` 或者 `scp` 的时候，为了减少输入量和降低输入错误的概率，可以为常用的远程主机设置别名。

方法是修改 `~/.ssh/config` 文件（如果不存在这个文件则创建），指定以下几个字段值即可：

```
host {自定义的主机别名}
hostname {主机的 IP}
port {连接主机的端口}
user {连接主机的用户名}
```
