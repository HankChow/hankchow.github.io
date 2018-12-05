---
title: Saltstack 初始化部署
date: 2018-12-01 14:26:12
tags:
  - Linux
  - Python
  - Saltstack
---

主控端安装 salt-master：

```shell
yum install -y salt-master
systemctl enable salt-master.service
systemctl start salt-master.service
```

被控端安装 salt-minion：

```shell
yum install -y salt-minion
systemctl enable salt-minion.service
systemctl start salt-minion.service
```

在主控端添加 TCP 4505、TCP 4506 的规则，在被控端无需配置防火墙。原理是被控端直接与主控端的 zeroMQ 建立长连接，接受广播到的任务信息并执行。

```shell
iptables -I INPUT -m state --state new -m tcp -p tcp --dport 4505 -j ACCEPT
iptables -I INPUT -m state --state new -m tcp -p tcp --dport 4506 -j ACCEPT
```

在主控端进行角色配置，修改主控端配置文件 `/etc/salt/master`：

```
interface: {主控端 IP 地址}

# 自动认证，如果不打开，需要通过 `salt-key -a {id}` 进行 key 的认证
auto_accept: true

# 指定 Saltstack 文件根目录位置
file_roots:
    base:
        - /srv/salt
```

然后重启主控端的 Saltstack 服务。

在被控端进行角色配置，修改被控端配置文件 `/etc/salt/minion`：

```
master: {主控端 IP 地址}

# 修改被控端主机识别 id
id: {id}
```

然后重启被控端的 Saltstack 服务。
