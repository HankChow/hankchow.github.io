---
title: Linux 下普通用户获取 sudo 权限的方法
date: 2018-12-01 12:09:55
tags:
  - Linux
---

在 Linux 创建新用户后，如果需要使该用户能以 `sudo` 方式执行命令，需要把用户添加到 `sudoers` 文件中，否则在使用 `sudo` 的时候会报“{user} is not in the sudoers file”错误。此时需要将用户添加到 `sudoers` 文件中，并使其获得相应权限。

首先需要使用 root 用户，执行命令：

```shell
visudo
```

打开 `sudoers` 文件，然后在其中添加

```
{user} ALL=(ALL:ALL) ALL
%{user} ALL=(ALL) NOPASSWD: ALL # 设置{user}组下面的用户使用 sudo 不需要输入密码
```

保存后，该用户即可使用 `sudo` 命令。

4个 ALL 之中，第 1 个 ALL 是用户(user)，第 2 个 ALL 是机器，第 3 个 ALL 是新用户身分(run_as_user, 如 root, oracle)，第 4 个ALL 是命令。
