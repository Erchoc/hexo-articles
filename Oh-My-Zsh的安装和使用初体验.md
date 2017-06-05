---
title: Oh_My_Zsh的安装和使用初体验
date: 2017-05-14 16:12:05
tags: tools
---

> 在实验楼的官方QQ群和人家吹牛逼时候学到了几点东西：windows子系统linux仿终端开源软件wsl，最新windows10 1703内置ubuntu16.04，听说支持在linux中打开exe可执行文件，编译安装vim以执行python lua补全和异步代码测试，公司服务器可能运行着Arch这等神器，据说今年Build大会微软会推出安装Fodora和Suse，VirtualBox和VMware虚拟机作用可以使用Hyper-V+Docker替代，最重要的一点是他让我知道了：Oh-My-Zsh主题是可以安装在Windows-Linux-MacOS 三大平台的！

> 那我就不得不尝试一下了，官网在这里：http://ohmyz.sh/ 。考虑到没几个月我就会转向MacOS上开发，这次我就打算先双系统更新到WIN10 1703，使用wsl终端+子系统Ubuntu 16.04+Zsh Shell。

<!-- more -->

- OS X用户：睾贵的自带了zsh，跳过...

- Ubuntu用户：sudo apt-get install zsh

- Windows老用户：由于天生太高贵，无法安装。

- Windows 10推出了bash for windows，终于也可以使用zsh

- 装上1703之后我不得不说这个版本确实更新挺大，很值得升级！默认使用powershell代替cmd提示符，ubuntu子系统可以选择中文，php源仓库中默认版本为php7，默认还有游戏模式，邮件直接支持注册Gmail账户，太多好处了，下面我们还是先说说zsh这个高效主题吧吧。

- 首先当然是去开源的代码托管平台看看这个star数超过50K的Oh-My-Zsh项目，要知道laravel也才30K。源码地址：https://github.com/robbyrussell/oh-my-zsh 。

- 然后当然是windows上安装这东西的步骤

```
查看系统中有哪些shell？
cat /etc/shells

搜索看看仓库里和zsh相关的包有哪些？
sudo apt-cache search zsh

看到了包的说明后，我们看看zsh包详细说明。
sudo apt-cache show zsh

看到我们即将安装的是最新版本5.0，然后安装zsh这个SHELL。
sudo apt-get install zsh -y

验证下安装是否成功。
zsh –version

查看当前的默认shell是啥。
echo $SHELL

是bash。那么我们把默认SHELL改成zsh吧。
chsh -s $(which zsh)
```
- 上面最后部分的操作可能在windows内置子系统中并不生效，那么我们可以在.bashrc末尾加上shell代码，用脚本实现当你打开bash时候切换到zsh。

```
bash -c zsh
```
- 退出后重新登录，查看默认shell。windows用户就不用查看shell了，永远只能看到默认的bash。

- 默认情况下用户主目录会生成.oh-my-zsh目录，.zsh_history，.zshrc和.zsh -update文件，.zcompdump文件，他们的作用和bash类似，分别是，`oh_my_zsh主题配置文件夹`, `记录用户历史执行的命令`, `zsh启动时加载的配置文件`,`记录更新操作`和这种dump文件我也不知道是啥了。

- 关于zsh主题和插件

- zsh默认主题是robbyrussell，位于主目录.zshrc文件中，下面我们来修改一下zsh的主题。

- 找到.zshrc文件中的ZSH_THEME="xxxx"，修改为下列我使用后推荐的主题或随机主题random。

```
ZSH_THEME=”random”
ZSH_THEME=”agnoster”
ZSH_THEME=”ys”
ZSH_THEME=”sorin”
ZSH_THEME=”cloud”
```

- 更多主题效果查看(按英文字母排序)：https://github.com/robbyrussell/oh-my-zsh/wiki/themes 。

- 另外，zsh自带Git命令哦，Ubuntu 16.04实测自带git版本还挺新 2.7.4。

- 主题主要是界面，好看就行。实用的还是zsh的插件哦，zsh插件太多了，暂时我也没接触多少，留着以后的文章再提吧。

- 关于zsh完美搭档git和iTerm2

- zsh利用alias默认给你配置好了一大堆用于git操作的常见命令，你能用上几个技术水平哦，贴图：

![Oh_My_Zsh已有Git系列的别名](http://upload-images.jianshu.io/upload_images/3995745-542011a4e02aea1d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 其他一些注意事项

```
zsh在其实默认不完全兼容bash，但是你可以搜索一些方式配置使其尽可能兼容。

zsh提供了很多短小但是强大的命令，zsh的拓展命令很多也非常强大，这点我也在慢慢学习。

关于iTerm2配合使用在另一篇文章有写过，强大工具！
```