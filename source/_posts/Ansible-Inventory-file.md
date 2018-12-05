---
title: Ansible Inventory 文件
date: 2018-11-30 10:07:21
tags:
  - Ansible
---

Ansible 的 Inventory 文件主要记录了连接主机的信息和配置，默认路径为 `/etc/ansible/hosts`。

在 Inventory 文件中以行为单位直接写入主机的 `host`，如果仅填写了 `host`，则其它信息均按照默认值（如 ssh 端口为22）。也可以按照组的格式进行配置：

```
[group1]
host1
host2

[group2]
host2
host3

[group3:children]
group1
group2
```

同一个主机可以同时属于多个组，如 host2 可以同时属于 group1 组和 group2 组。组也可以作为另一个组的成员，如 group1 和 group2 就是 group3 的成员，因此 host1、host2、host3 均属于 group3 组。

在每个 host 后可以使用变量来设置一些具体的参数，例如端口、登录用户名等。也可以为整个组设定变量：

```
[group1:vars]
ansible_ssh_port=2222
ansible_ssh_user=root
```

常用的 Inventory 参数：

```
ansible_ssh_host
      将要连接的远程主机名.与你想要设定的主机的别名不同的话,可通过此变量设置.

ansible_ssh_port
      ssh端口号.如果不是默认的端口号,通过此变量设置.

ansible_ssh_user
      默认的 ssh 用户名

ansible_ssh_pass
      ssh 密码(这种方式并不安全,我们强烈建议使用 --ask-pass 或 SSH 密钥)

ansible_sudo_pass
      sudo 密码(这种方式并不安全,我们强烈建议使用 --ask-sudo-pass)

ansible_sudo_exe (new in version 1.8)
      sudo 命令路径(适用于1.8及以上版本)

ansible_connection
      与主机的连接类型.比如:local, ssh 或者 paramiko. Ansible 1.2 以前默认使用paramiko.1.2 以后默认使用 'smart','smart' 方式会根据是否支持 ControlPersist, 来判断'ssh' 方式是否可行.

ansible_ssh_private_key_file
      ssh 使用的私钥文件.适用于有多个密钥,而你不想使用 SSH 代理的情况.

ansible_shell_type
      目标系统的shell类型.默认情况下,命令的执行使用 'sh' 语法,可设置为 'csh' 或 'fish'.

ansible_python_interpreter
      目标主机的 python 路径.适用于的情况: 系统中有多个 Python, 或者命令路径不是"/usr/bin/python",比如  \*BSD, 或者 /usr/bin/python
      不是 2.X 版本的 Python.我们不使用 "/usr/bin/env" 机制,因为这要求远程用户的路径设置正确,且要求 "python" 可执行程序名不可为 python以外的名字(实际有可能名为python26).

      与 ansible_python_interpreter 的工作方式相同,可设定如 ruby 或 perl 的路径....
```
