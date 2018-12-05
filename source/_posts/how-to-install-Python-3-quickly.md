---
title: 在新机器上快速安装 Python 3
date: 2018-11-29 13:55:31
tags:
  - Linux
  - Python
  - 快速安装
---

对于以 Python 3 为主力开发语言的人来说，在一台新的机器上必须尽早安装上 Python 3。而对于绝大多数 Linux 发行版来说，都只默认安装了 Python 2 而没有 Python 3，而且有一些 Linux 自带的命令（例如 `yum`）会依赖 Python 2，这就需要在安装 Python 3 的同时保留 Python 2，并且使两者区分开来。

快速安装如下：

```shell
# 版本号
version="3.6.2"

# 安装依赖包
yum -y groupinstall "Development tools"
yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel

# 下载 Python 3 源码，版本号可改
which wget || yum -y install wget
wget https://www.python.org/ftp/python/$version/Python-$version.tar.xz

# 解包、编译、安装
mkdir /usr/local/python3
mv ./Python-$version.tar.xz /usr/local/python3
cd /usr/local/python3
tar -xvJf  Python-$version.tar.xz
cd Python-$version
which gcc || yum install -y gcc
./configure --prefix=/usr/local/python3
make && make install

# 设定 Python 3 和 pip3 的软连接
ln -s /usr/local/python3/bin/python3 /usr/bin/python3
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3
```
