---
title: 如何在 CentOS 7 上手动搭建 LAMP 环境
date: 2018-11-29 10:00:58
tags: 
  - Apache
  - LAMP
  - MySQL
  - PHP
---

拿到一台新的服务器之后，如果要搭 WordPress 之类的服务，就需要搭建一个 LAMP 环境。

鉴于网上各种一键 LAMP 的质量稂莠不齐，自己搭一个还是比较妥当的做法，而且后续如果需要自定义配置的话更加方便，不至于发生太多关于包依赖的问题。

```shell
# 安装 Apache
yum -y install httpd
# 启动服务
systemctl start httpd.service
# 设置开机自动启动
systemctl enable httpd.service
 
# 安装 MySQL（在 CentOS 7 上其实是 MariaDB，但兼容 MySQL）
yum -y install mariadb mariadb-server
# 启动服务
systemctl start mariadb.service
# 设置开机启动服务
systemctl enable mariadb.service
# 设置数据库管理员密码
mysql_secure_installation
 
# 安装 PHP
yum -y install php
# 安装各种 PHP 的组件
yum -y install php-gd php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-snmp php-soap curl curl-devel php-mysql
# 重启一下
systemctl restart httpd.service
```

这样基本就可以直接安装 WordPress 了。
