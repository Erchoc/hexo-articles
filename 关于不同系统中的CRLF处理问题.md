---
title: 关于不同系统中的CRLF处理问题
date: 2017-06-06 09:07:08
tags: 操作系统
---

> 昨天胖子在群里问了个`git add`将代码从工作区加入暂存区时出现CRLF和LF转换的问题，正好一年前我刚玩linux时候研究过一阵子这个问题，今天早上使用tcg/voyager时候也出现了这个问题，这里我就稍微说一下问题出现的原因以及处理的办法。

> 如果您在Windows上进行编程，但你的合作团队有人在MacOS或者Linux上编程，你可能遇到这篇文章的说明问题。这是因为Windows在其文件中使用换行符和换行字符，而Mac和Linux系统只使用换行字符。这是跨平台工作令人难以置信的烦人事实; Windows上的许多编辑器用CRLF替换现有的LF行的结尾，或者当用户点击Enter键时插入两个行结束字符

<!-- more -->

- 首先我们必须知道现在电脑系统有windows，unix两大系列，unix下有很多变体称为`类Unix系统`，主要有MacOS，Linux，Hp-ux，Ibm-aix，Solaris等等。这其中由于Linux是开源集大成者，在它的体系中又衍生了以Fodora和Debian的两大阵营。类unix系统大多数时候是使用兼容的，但是windows和类unix系统之间无论是操作还是设计理念都不一样。

- 这次要提到的问题，起源就在上面这段话中。类unix系统中，回车就是回车(carriage return)，换行就是换行(line feed)，它们绑定13和10两个ASCII码值，回车和换行分别简称CR和LF。编辑代码的时候，Windows系统里面，每行结尾是"<回车><换行>"，即"\r\n"；类Unix系统里，每行结尾是"<回车>"。

- 这样会导致什么后果？Unix/Mac系统下的文件在Windows里打开的话，所有文字会变成一行；而Windows里的文件在Unix/Mac下打开的话，在每行的结尾可能会多出一个^M符号。

- 那么胖子的`git add`操作中为什么会提示LF将会被替换为CRLF呢？主要可能有下面几个原因？
  - 团队开发，每个人实用的操作系统平台不同。
  - 胖子使用了双系统，开发时候切换系统进行编码。
  - 没有设置PhpStorm和Atom等常用IDE均有的LF绑定功能。

- 解决办法呢？主要看你从git角度去解决还是文件角度去思考。如果你想把文件本身进行转换，请使用`IDE的LF-CR绑定设置`或者`.editorconfig`文件转换，如果你从代码提交暂存区或者仓库来考虑，那么Git有几个配置选项来帮助解决这些问题，你应该看看下面的几行代码：
```
git config core.autocrlf true

git config core.autocrlf input

git config core.autocrlf false
```

> core.autocrlf这个设置应该在Windows检查中留下CRLF结尾，但是在Mac和Linux系统以及存储库中的LF结束。

- 第一行：当你将文件添加到暂存区时，Git可以通过设置core.autocrlf将CRLF行结尾自动转换为LF来处理这类问题。如果您在Windows机器上，将其设置为true，那么当您pull代码时，将LF结尾转换为CRLF。

- 第二行：如果您使用的是Linux或Mac系统，那么当您pull文件时，您不希望Git自动转换它们; 然而，如果你的Windows猪队友把未经处理带CRLF格式的文件push到远程代码库，那么你可能希望Git来自动解决这个问题。可以通过将core.autocrlf设置为input来告知Git将CRLF转换为LF。

- 第三行：如果你是Windows程序员，只执行一个Windows项目或者所团队都是用windows系统甚至服务器都用windows，那么您可以关闭此功能，通过将配置值设置为false，将回车记录在存储库中。

- 参考地址：
  - [阮一峰网络日志](http://www.ruanyifeng.com/blog/2006/04/post_213.html)
  - [维基百科：类Unix系统](https://zh.wikipedia.org/wiki/%E7%B1%BBUnix%E7%B3%BB%E7%BB%9F)