---
title: CentOS 7 上的 systemctl 配置
date: 2016-09-09 10:07:54
tags:
  - Linux
---

CentOS 7 的服务 `systemctl` 脚本存放在目录 `/usr/lib/systemd/` 下，有系统（system）和用户（user）之分，需要开机不登陆就能运行的程序，存在系统服务即 `/usr/lib/systemd/system/` 目录下。

CentOS 7 的每一个服务以 .service 结尾，一般会分为 3 部分：[Unit]、[Service] 和 [Install]。

[Unit]部分主要是对这个服务的说明，内容包括Description和After，Description 用于描述服务，After用于描述服务类别

[Service]部分是服务的关键，是服务的一些具体运行参数的设置。
Type=forking 是后台运行的形式，
User=users 是设置服务运行的用户,
Group=users 是设置服务运行的用户组,
PIDFile 为存放 PID 的文件路径，
ExecStart 为服务的具体运行命令,
ExecReload 为重启命令，
ExecStop 为停止命令，
PrivateTmp=True 表示给服务分配独立的临时空间。

[Install]部分是服务安装的相关设置，可设置为多用户的。

注意：[Service]部分的启动、重启、停止命令全部要求使用绝对路径，使用相对路径则会报错。
