---
title: Docker 运行官方 MySQL 镜像无法远程连接的坑
date: 2018-12-01 14:28:52
tags:
  - Docker
  - MySQL
  - 坑
---

使用 Docker 官方提供的 MySQL 镜像进行安装、建立容器（必须指定端口映射和 root 口令）。

```shell
docker pull mysql:latest
docker run -p 9527:3306 -e MYSQL_ROOT_PASSWORD=root -d mysql
```

但此时如果直接远程连接该容器中的 MySQL 并输入口令后，则会出现报错信息：

```
ERROR 2059 (HY000): Authentication plugin 'caching_sha2_password' cannot be loaded: /usr/lib64/mysql/plugin/caching_sha2_password.so: cannot open shared object file: No such file or directory
```

根据报错信息，连接失败原因为口令使用了 `caching_sha2_password` 方式进行加密，通过 `SELECT user, host, plugin, authentication_string FROM user WHERE user='root';` 查询可以看到 root 用户的口令确实是使用 `caching_sha2_password` 方式进行加密，而客户端找不到 `caching_sha2_password` 插件，因此连接失败。

根据官方文档，可以将加密方式更改为 `mysql_native_password`。通过 `ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root';` 将 root 用户的口令加密方式更改为 `mysql_native_password`，在远程即可正常连接 MySQL。
