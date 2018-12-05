---
title: Ansible 的各个模块及相关参数
date: 2018-12-01 12:08:32
tags:
  - Ansible
---

* command：在被控节点上执行命令
  * command 是 Ansible 的默认模块，可以不通过 -m 指明使用该模块
  * 可以直接执行 -a 中的命令，但由于不通过 shell 执行，所以与 shell 有关的变量、重定向、管道等功能无法使用
  * kwargs：
    * chdir：目录名。首先跳转到该目录后再执行命令
* shell：在被控节点上通过 shell 执行命令
  * 与 command 模块基本相同，而且由于通过 shell 执行，所以可以使用变量、重定向、管道等功能，并且使用所选用户的默认 shell
  * kwargs：
    * chdir：目录名。首先跳转到该目录后再执行命令
* script：在被控节点上执行主控节点上的脚本
  * 直接在 -a 中指明主控节点上的脚本位置即可，且这个脚本需要有 x 权限
* ping：检测某个目的节点是否响应
  * 这个检测过程并不向目的节点发送 ping 包，只是反映目的节点是否可控，目的节点即使在可达的情况下也不一定可控
  * 不指定 -a
* yum：在被控节点上通过 yum 管理软件
  * kwargs：
    * name：软件包名称。如果为 * ，则执行 yum -y updtae；名称前面加 @ 为安装软件包组；名称前面加 @^ 为安装环境组；这个参数也可以是 url，此时通过指定的 rpm 文件进行安装
    * state：软件安装状态。如果为 present、latest 或 installed 则执行安装软件；如果为 absent 或 removed 则执行移除软件
* copy：从主控节点向被控节点复制文件
  * kwargs：
    * src：主控节点的文件位置。可以是绝对路径或相对路径，如果是一个目录，将会进行递归复制
    * dest：被控节点的文件位置。必须为绝对路径，且如果 src 是一个目录，dest 也必须为一个目录
    * directory_mode：递归设定目录的权限。默认为系统默认权限
    * force：是否覆盖。默认为 yes，即当目标文件和源文件不同时，强制覆盖文件，如果为 no 则只有在目标文件不存在时才复制
* fetch：从被控节点向主控节点复制文件
  * 与 copy 模块并不仅仅是方向相反，copy 可以复制文件和目录，而 fetch 模块只能复制文件
  * kwargs：
    * src：被控节点的文件位置。
    * dest：文件在主控节点中的保存位置。真实的保存目录需要注意，如果指定了 dest 参数为 /foo，被控节点为 bar，则文件将会保存在 /foo/bar/ 下
    * fail_on_missing：被控节点中的文件不存在时是否报错。默认为 no，当为 no 时即使文件不存在也不会报错，此时主控节点也不会创建相应的目录
* synchronize：通过 rsync 传输文件
  * kwargs：
    * src：源文件的位置。
    * dest：目标文件的位置。
    * mode：推送模式或拉取模式。默认为推送模式 push，从主控节点向被控节点传输文件
    * delete：是否删除文件使两方一致。两方的一致性以推送方为准，默认为 no
* service：用于管理服务
  * kwargs：
    * name：服务名称。
    * state：对服务的操作。包括启动(started)、停止(stopped)、重启(restarted)、重新加载(reloaded)
    * enabled：是否开机启动。且 state 和 enabled 两个参数中至少要有一个
    * sleep：在 state=restarted 的时候，指定在 stop 和 start 之间暂停的秒数
* get_url：通过 http/https/ftp 下载文件
  * kwargs：
    * url：下载的 uri
    * dest：文件下载目标位置。如果 dest 为目录，则使用服务器提供的文件名，或者如果没有提供，将使用远程服务器上的 url 的基本名称。
    * timeout：设置超时时间。默认为 10s
    * headers：指定访问时的请求头。以 key: value 的格式填写

