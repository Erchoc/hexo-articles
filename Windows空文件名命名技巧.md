---
title: Windows空文件名命名技巧
date: 2017-05-08 16:08:10
tags: skills
---

> 如何将文件名设置为空，这是个不得不说的程序员大事。在类Unix的Linux和MacOS上完全不用担心这个问题，但是windows底层设计不允许直接新建有后缀没名字的文件和文件夹。CodeIgniter和Apache的.htaccess重写，laravel5在github上的源码直接clone下来无法使用，因为项目目录下的.env.example在windows系统下无法重命名为.env。这都是windows诟病导致的一些开发环境问题。

> 关于文件命名为空有很多种方法，普通用户用windows系统自带的charmap字符映射表替换为空格即可。但是开发者需要的是实实在在的空文件名，最简单的做法是压缩这个文件，在压缩文件内重命名后再解压。

> 另外，开发者应该都会使用git，模拟unix环境的终端里面可以使用touch新建空文件名，也可以使用mv修改为空。

<!-- more -->

- win10开发者模式下自带的ubuntu bash也同样可以执行这些命令修改为空文件名。

- 当然，你也可以使用bat批处理文件的替换脚本。

- 你甚至可以直接在sublime中新建命令为空的文件。

- 关于使用github上laravel源码的问题，由于官方源码并没有生成base64的APP_KEY，也没有包含各种依赖文件。

- 所以git clone后你要做的就是进入这个项目目录修改.env.example文件为.env。然后执行composer install。

- 之后还是无法访问public目录，并且没有详细报错信息，这时你应该打开config/app.php文件，将debug设置为true再刷新页面。你会看到关于解码的错误，这时你应该在项目根目录打开控制台输入php artisan key:generate。

- 你会看到.env文件中的APP_KEY生成，页面可以正常使用了。

- 上面的做法结束后你还应该替换.git文件夹，配置提交到自己的仓库。还是建议使用composer create-project而不要使用laravel安装器安装框架，主要还是因为composer安装会有自带脚本重命名.env文件并生成唯一密钥。
