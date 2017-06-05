---
title: CentOS服务器部署
date: 2017-05-08 16:07:53
tags: linux
---

> 测试服务器使用的bandwagonhost最小化安装的CentOS7，纯净到连管理权限的sudo命令都没有。

> 购买该服务器后得到ip地址和ssh开放端口以及root用户的密码(随机密码)。打开终端或者命令提示符，windowsy用bash切换到内部子系统ubuntu再用ssh命令连接到服务器：

```
ssh -p $port root@$ip
```
> 剪切密码，接受并保存本地密钥（如果密钥改变，请手动删除～/.ssh/$pubKey）。

<!-- more -->

- 安装sudo库，useradd和passwd新建用户设置密码

```
yum install sudo -y

useradd yanggege

passwd yanggege

id yanggege
```

- 把这个用户添加到wheel root用户组

```
usermod -g root yanggege。
```

- 由于sudo命令的问题，在sudoers文件中限制了用户访问的权限。所以我们使用root行复制改名的方法，也可以选择添加或者打开wheel组权限。

```
vi /etc/sudoers
```

- yum源的问题

```
centos,RHEL和Fodora同属于RedHat系列，另一主要阵营是Debian的ubuntu系列。

前者的数据软件仓库叫做yum源，安装软件也是使用yum install命令。

默认的centos官方源在国外，下载速度慢。

国内阿里云和各高校提供了免费的yum源，建议更换为国内的网易开源镜像站地址。。
```
- 更换默认yum源为网易镜像站点的纯小白教程：http://mirrors.163.com/.help/centos.html。

- 根据你的服务器系统版本顺序执行mv备份，wget下载(在这个目录下执行哦：/etc/yum.repos.d/)，yum清除缓存几条命令即可。

- 安装软件步骤：一更新，二有无，三信息，四下载安装

```
yum update

yum search git

yum info git

yum install git -y

-y参数代表直接安装，不写就会提示需要安装一些依赖，你要不要安装？

建议初学都不加该参数，自己看看依赖哪些包也是极好的。

如果你想同时安装多个软件，可以这样：yum install docker.io git gcc。
```

- 查看安装是否成功

```
git --version
```

- centos是很多大企业再用的服务器系统，重在稳定，官方提供的yum包一般版本偏低。

yum其实是下载的rmp格式的包进行shell脚本自动化操作，你也可以自行下载更高版本的rpm包，再将其添加到本地仓库安装。

- 卸载git或者其他软件

```
yum deplist git

yum remove git
```

- 查看yum安装的软件列表和某软件信息

```
yum list

yum list git

yum list不带软件包名将列出所有使用yum安装的包，包括很多依赖包，请谨慎使用

配合linux中的head,tail和grep命令使用就不担心输出内容可能过多的问题。
```

- 我常用的yum源命令就上面这些了，其他很多命令你都可以使用–help或者man查看文档。
