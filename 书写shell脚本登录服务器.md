---
title: 书写shell脚本登录服务器
date: 2017-05-26 12:42:29
tags: linux
---

> 本文主要讲解使用shell脚本登陆远程服务器, 解放大脑记忆ip地址的局限性。shell只是一类语言的总称，这类语言有类似的历史，类似的语法，甚至相互之间还能兼容。

<!-- more -->

- 首先是ssh正常登陆命令。

```
ssh -p port user@remoteip
```

- 容易忘记ip吖, 那么我们写成简单的shell脚本。`cd && vim bwg.sh`

```
\#!/bin/bash

ssh -p port user@remoteip
chmod +x bwg.sh
./bwg.sh
```

- 不想每次都输入密码？ 那我们来配置公钥和私钥。

```
本机生成公钥和私钥请输入`ssh-keygen`

三次回车生成`id_rsa`和`id_rsa_pub`。

将公钥传送到远程主机host上面：

`ssh-copy-id user@remoteip -p port`

配置完成, 下面测试一下: `./bwg.sh`
```

- 确实不用输入密码就成功了, 不记得有`ssh-copy-id`, 你也可以执行这句代码代替:

- ssh user@remoteip 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub`

