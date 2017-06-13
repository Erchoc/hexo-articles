---
title: 直推！Git服务器的搭建
date: 2017-05-16 06:13:00
tags: linux
---

> GitHub就是一个托管代码的远程仓库。但是对于某些公司项目来说，既不想公开源代码，又舍不得给GitHub交私有仓库管理费用，也不屑于使用国内的码云等平台，那就只能自己搭建一台Git服务器作为私有仓库使用。

> 搭建Git服务器需要准备一台运行Linux的机器，推荐使用Ubuntu或Debian，配合Docker集成文件监听，可以完美实现DevOps模式和无痛迭代。可是，Docker并不在本文的讨论范围哦。

> 假设你已经登录了有sudo权限的用户账号，下面，正式开始安装。当然这里我们也可以在自己的服务器上安装具有更多功能的GitLab。

<!-- more -->

### 第一步，安装git：

```
sudo apt-get install git
```

### 第二步，创建一个git用户，用来运行git服务：

```
sudo adduser git
```

### 第三步，创建证书登录：

```
收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件。

把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。
```

### 第四步，初始化Git仓库：

```
选一个目录作为这个项目的Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：

sudo git init --bare sample.git

这样，Git就会创建一个裸仓库，裸仓库没有工作区。

服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区。

把owner改为git：

sudo chown -R git:git sample.git
```

### 第五步，禁用shell登录：

```
安全考虑，第二步创建的git用户不允许登录shell，可以编辑/etc/passwd文件完成禁止。

找到类似下面的一行：

git:x:1001:1001:,,,:/home/git:/bin/bash

改为：

git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell

这样，git用户可以正常通过ssh使用git，但无法登录shell。

因为我们为git用户指定的git-shell每次一登录就自动退出。
```

### 第六步，克隆远程仓库：

```
现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：

git clone git@server:/srv/sample.git

Cloning into 'sample'...
warning: You appear to have cloned an empty repository.

剩下的项目开发代码推送就简单了，和你使用Github是一样的。
```

### 第七步，管理公钥

```
小团队把每个人的公钥收集放到服务器的/home/git/.ssh/authorized_keys文件里就行。

如果团队有几百号人，就没法这么玩了，这时，可以用Gitosis来管理公钥。

这里就不介绍怎么使用Gitosis了，几百号人的公司找个高水平的Linux管理员问题不大。
```

### 第八步，管理权限

```
有些视源码如生命，视员工为窃贼的公司，会在版本控制系统里设置一套完善的权限控制。

每个人是否有读写权限会精确到每个分支甚至每个目录下。

因为Git是为Linux源代码托管而开发的，所以Git继承了开源社区的精神，不支持权限控制。

但Git支持钩子(hook)，可以在服务器端编写脚本来控制提交等操作，达到权限控制的目的。

Gitolite就是一个这样的控制权限的工具。

这里我们也不介绍Gitolite了，不要把有限的生命浪费到权限斗争中。
```

### 第九步，小结

```
搭建Git服务器非常简单，通常10分钟即可完成；

要方便管理公钥，用Gitosis；

要像SVN那样变态地控制权限，用Gitolite。
```
