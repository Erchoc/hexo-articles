---
title: Vim学习第三步是插件
date: 2017-06-08 11:47:01
tags: 高效工具
---

> 当然，你会用vim自带的配置提高工作效率了，可你能够配置个Emmet出来吗？你能配置个Xdebug出来吗？强大的vim强在它的生态系统上，无数的插件都有支持vim的版本哦。

> 现在到处都流行组件化思想了，我们的vim好早就支持各种插件就是一种组件化。这里我们来试试插件的管理和安装。

 <!-- more -->

 - vim是vi命令的升级版，总之就是各种更强且兼容。那么如果你使用linux系统，可能需要`sudo yum install vim -y`或者`sudo apt-get install vim -y`下载一下。

 - vim是一个在命令行模式编辑文件的软件，它有个全局配置文件和用户级配置文件.vimrc。主要用于多用户的linux服务器上它们分别位于`/usr/share/vim/vimrc`和`~/.vimrc`。

- 举个例子来看看我这里的vim全局配置文件吧:前面是vim默认打开的xitong，后面set开始都是我添加的设置语法高亮，Tab长度，智能缩紧等等。

- 但是MacOS作为个人电脑，默认情况并没有用户级配置文件，你可以自行建立配置文件和文件夹进行vim相关的管理：
```
cd && mkdir vim

cp /usr/share/vim/vimrc ~/.vimrc
```