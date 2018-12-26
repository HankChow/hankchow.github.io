---
title: 如何安装及管理 Ruby
date: 2018-12-26 01:55:06
tags:
  - Ruby
---

可以使用 rvm 管理 Ruby 及其软件包。

预先安装 Ruby 需要使用到的软件包：

```
yum install -y gcc-c++ patch readline readline-devel zlib zlib-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison iconv-devel
```

使用 rvm 官方提供的脚本安装 rvm：

```
curl -L get.rvm.io | sh -s stable
```

如果按照以上命令安装 rvm 失败，需要使用以下方式更新相关证书：

```
curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -
curl -sSL https://rvm.io/pkuczynski.asc | gpg2 --import -
```

证书更新之后再次执行 `curl -L get.rvm.io | sh -s stable` 安装 rvm。安装完成时候可以设置 `rvm` 命令：

```
source /etc/profile.d/rvm.sh
```

查看当前 Ruby 版本：

```
ruby -v
```

使用 rvm 安装指定版本的 Ruby：

```
rvm install {ruby_version}
```

如果安装过程太慢，可以考虑切换到其它安装源镜像，在 `/usr/local.rvm/user/db` 文件中加入：

```
ruby_url={ruby_source_url}
```

即可。
