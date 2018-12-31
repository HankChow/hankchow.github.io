---
title: 快速安装 zsh
date: 2017-04-28 12:10:27
tags:
  - zsh
---

在新机器上快速安装比 bash 不知道高到哪里去了的 zsh。

```shell
# 安装 zsh
yum -y install zsh
# 把默认 shell 替换为 zsh
chsh -s /bin/zsh

# 安装 oh-my-zsh
which curl || yum -y install curl
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
```
