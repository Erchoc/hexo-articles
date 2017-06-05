---
title: Linux下PATH变量和Composer的操作问题
date: 2017-05-07 16:09:38
tags: linux
---

> PATH就是操作系统中的环境变量，无论是windows，linux还是macos都存在这个环境变量。它存储着一些目录的集合，决定着shell将到哪些目录中寻找命令或程序，PATH的值是一系列目录，当你运行一个程序时，Linux首先在环境变量下进行搜寻程序，找不到则执行当前目录下能对应的程序，没有的话终端界面就返回Not Found或者Command Not Exists提示。

<!-- more -->

- 添加某个目录dire到环境变量，其格式为：PATH=dire:$PATH。环境变量更改后，在用户下次登陆时生效，如果想立刻生效，则可执行下面的语句：

```
source .bash_profile
```

- 需要注意的是，最好不要把当前路径 “./” 放到 PATH 里，这样可能会受到意想不到的攻击。

- 完成后，可以通过 echo $PATH 查看当前的搜索路径，即环境变量值。

- 可用 export 命令查看PATH值

```
yangxuejin@THINKPAD_X220:/mnt/d/OneDrive/WWW$ export
declare -x HOME="/home/yangxuejin"
declare -x HOSTTYPE="x86_64"
declare -x LANG="en_US.UTF-8"
declare -x LESSCLOSE="/usr/bin/lesspipe %s %s"
declare -x LESSOPEN="| /usr/bin/lesspipe %s"
declare -x LOGNAME="yangxuejin"
declare -x LS_COLORS="rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arj=01;31:*.taz=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.dz=01;31:*.gz=01;31:*.lz=01;31:*.xz=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.jpg=01;35:*.jpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.axv=01;35:*.anx=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.axa=00;36:*.oga=00;36:*.spx=00;36:*.xspf=00;36:"
declare -x NAME="THINKPAD_X220"
declare -x OLDPWD
declare -x PATH="/home/yangxuejin/.composer/vendor/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games"
declare -x PWD="/mnt/d/OneDrive/WWW"
declare -x SHELL="/bin/bash"
declare -x SHLVL="1"
declare -x TERM="xterm"
declare -x USER="yangxuejin"
```

- 单独查看PATH环境变量，可用：

```
echo $PATH
```

- 下载composer.phar文件

```
cd && wget https://getcomposer.org/composer.phar
```

- 移动到$PATH目录下的同时修改文件名

```
mv composer.phar /usr/local/bin/composer
```

- 测试composer并查看和修改默认的仓库repository

```
composer -–version

composer config -g repo

composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

- 使用composer搜索thinkphp项目和查看版本详情

```
composer search thinkphp

composer show --all topthink/thinkphp
```
- 使用composer创建thinkphp5项目

```
composer create-project topthink/thinkphp tp3

composer create-project topthink/think tp5
```

- 安装并临时修改环境变量测试laravel安装器：

```
composer global require “laravel/installer”

PATH=/home/yangxuejin/.composer/vendor/bin:$PATH

laravel –-version
```
- 上述方法的PATH在终端关闭后就会消失。所以还是建议通过编辑/etc/profile来改PATH，用户级就是修改家目录下的.bashrc(即：~/.bashrc)。

- 永久添加PATH环境变量(系统级)，用户级.profile同理

```
sudo vim /etc/profile

export PATH=”/home/yangxuejin/.composer/vendor/bin:$PATH”

source /etc/profile
```

- 再次查看PATH：

```
echo $PATH
```