---
title: MacOS刚使用的几点问题
date: 2017-05-26 12:43:16
tags: tools
---

> Macbook Pro MF839昨天下午4点下单，今天下午4点收货，顺丰隔日速度值得表扬。开机配置，Apple id又被冻结了。激活之后查看电池使用次数为3，正品没毛病。然后就是安装各种软件了，PhpStorm，HomeBrew，git，Teambition，QQ，微信，WebStorm，shadowsocks，MAMP，VirtualBox，Chrome。

> 下面将会说到QQ语音视频没有声音和破解新版本MacOS10.11系统加入的SPI验证机制，并使用brew的增加版cask装了Docker-ce。

<!-- more -->

- 然后花了半个小时搞定了MAMP环境，真强，但是Sequel PRO官方下载也太慢了。MAMP PRO下载后会出现两个版本，你会发现收费版的MAMP PRO却可能无法使用，我在终端查看了两者目录的权限, 只有MAMP目录(/App/MAMP/htdocs/)属于当前用户访问。将就点用吧(最终我还是使用了破解版), 反正都是要过渡到Docker。

- 更新MacOS10.12和iWork等自带软件的时间最久了，总要来关机，还有漫长的更新时间。不是说苹果的Pcle固态速度比SATA3快至少两倍吗？

- 另外改hosts在苹果系统上刷新DNS并不是`ipconfig flushdns`也不是`sudo /etc/init.d/nscd restart`, 而是根据MacOS的版本选择不同的命令如:

```
Mountain Lion 或 Lion版本(10.7.8.9):
    sudo killall -HUP mDNSResponder
Snow Leopard版本(10.6.10):
    dscacheutil -flushcache
Leopard和更早版本(10.4.5):
    lookupd -flushcache

大概就是这样了, 更高版本也在里面选择。

吐槽以下Mac上这个刷新缓存很不统一啊
```

- 最后还是用了shadowsock自建的搬瓦工服务器，学习dockerfile之后有空就把shadowsock也写成文件容器来使用。

- 以前觉得自己黑苹果体验不佳是因为电脑差，现在买了正品才知道苹果系统在某些方面的等待时间确实偏久, 苹果的开机并不是非常快, 但是它可以不关机。虽然不喜欢的话好多操作的确不太人性化, 但习惯一下快捷键还是会很不错的。

- 项目还在开发我就换了电脑，虽然MacOS10.12自带php5.6，但我还是选择了MAMP搭建本地环境的过程就开始了。

-首先MAMP测试，修改默认端口访问localhost测试，然后添加hosts记录。

- 然后修改apache的vhost.conf文件，文件目录你可以根据apache全局配置文件中的引入路径查找。

- 另外使用了homebrew，操作了如下命令:

```
brew update    更新源
brew search wget  查找软件包
brew install wget  安装软件包
brew list    列出已安装的软件包
brew remove wget   删除软件包
brew info wget   查看软件包信息
brew deps wget   查看软件依赖关系
brew outdated    列出已安装但不是最新版本的软件包
brew upgrade wget   单个软件包更新

其实homebrew提供定制自己的软件包的功能哦，一切源自github。
```

- 没几天我尝试了下面这条命令, 结果Mac上我下载的软件视频和代码都消失了, 只好重装系统。

```
sudo rm -rf /

在Ubuntu服务器执行这条命令提示危险操作
```

- 重装系统后QQ视频聊天对方说我没有声音, 你可以在声音偏好设置的输出中选用Mac自带的内置扬声器, 我选择的是执行下面这条命令。

```
printf "p *(char*)(void(*)())AudioDeviceDuck=0xc3\nq" | lldb -n QQ
```

- 重装系统后因为要使用composer, 但意外的发现/bin/bin这样的环境变量下路径无权限访问。这是因为10.11开始加入的SIP验证机制, 我们只要重启进入命令行模式, 开机前将SIP关闭即可:

```
csrutil disable
```

- 还使用brew cask装了Docker-ce, 使用laradock单项目和多项目配置, 具体操作流程请看这篇文章:
http://www.jianshu.com/p/3b564f452625
