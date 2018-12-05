---
title: 在 WordPress 上在线安装插件的坑
date: 2018-11-29 10:38:25
tags:
  - PHP
  - WordPress
  - 坑
---

通过 WordPress 在线安装插件，目前遇到过两个坑：

* 如果通过 WordPress 在线安装插件，可能会遇到“无法连接到文件系统，请确认您的凭据”的提示。这种情况下一般不是 FTP 账号密码错误，而是安装插件所需要的操作权限不够。需要把 `wordpress/`、`wordpress/wp-content/`、`wordpress/wp-content/plugins/` 这三个目录的权限设置为 777，并且在配置文件 `wp-config.php` 中加入以下几行：

```php
define("FS_METHOD","direct");
define("FS_CHMOD_DIR", 0777);
define("FS_CHMOD_FILE", 0777);
```

* 开始安装后，可能会提示安装失败。这种情况下很可能是 DNS 被封的原因导致，把系统配置文件 `/etc/resolv.conf` 中的两个 `nameserver` 值改为 Google 的 8.8.8.8 和 8.8.4.4 后保存即可。
