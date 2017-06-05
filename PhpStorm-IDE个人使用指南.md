---
title: PhpStorm IDE个人使用指南
date: 2017-05-10 16:10:07
tags: tools
---

> 我是个PHP工程师，关于开发IDE的选用就PhpStorm不用争论了。很多人从DW或者Sublime转向PhpStorm时会发现很多快捷键都不一样，DW用户甚至都不怎么关注快捷键。PhpStorm快捷键大全自行Google就能找到，本文主要就是针对该IDE的快捷键和系统配置作个简要说明。

> PhpStorm 官方教程(英文)
[https://www.jetbrains.com/help/phpstorm/2017.1/meet-phpstorm.html]

> PhpStorm 使用教程Gitbook(中文)
[https://jellychendeveloper.gitbooks.io/phpstorm/content/]

<!-- more -->

- Ctrl+Z撤销过多步骤，Ctrl+Y却无法回退了。

```
反撤销快捷键为Ctrl+Shift+Z,你也可以修改键盘方案为Ctrl+Y。

查看菜单栏上的Edit->Redo Backspace就会显示反撤销快捷键Undo。
```

- 为我的项目重新命名，但是目录名不改变。

```
菜单栏File->Rename Project即可。

防止混淆项目，改成中文也不会有任何影响的。
```

- Project目录可以使用Shift+Esc关闭，那么使用什么快捷键打开呢？

```
Ctrl+Tab打开switcher，继续按住Ctrl+1打开Project。

Mac上使用Command + E进行切换，这也是工作文件切换的快捷键。
```

- 怎么匹配到A文件中所有的student字母并替换为teacher?

```
Ctrl+F搜索并选中一个student，然后Ctrl+Shift+Alt+J全部匹配同时修改。

这个快捷键可以修改为Ctrl+D选择单词，Ctrl+Alt+J全部匹配。
```

- Sublime文件切换有个Ctrl+P(Goto Anything)，PhpStorm呢？

```
Ctrl+Shift+N文件切换。
```

- PhpStorm侧边栏文件/目录重命名怎么操作？

```
右键要修改的文件/目录，选择Refactor->Rename，输入新名字即可。

默认的两个选项尽量勾选上，这样其他地方有引用这个文件/目录的话也会进行相应的改动。
```

- 选中Project文件，怎么打开所在目录？

```
Ctrl+Alt+F12，根据列表选择，如果要打开你选中的文件所在目录，直接回车即可。
```

- 怎么搜索并导入一个我喜欢的主题？

```
首先到这个网站下载一个你喜欢的主题。

然后在PhpStorm中点击File >> Import Settings选中确定重启即可。
```

- 怎么修改编辑代码区域和PhpStorm内置终端字体大小？

```
Ctrl+,打开Preferences，打开Editor >> Color & Fonts >> Font，双击右侧设置Size。

ctrl+,打开Preferences，搜索Console font，双击，右侧设置终端字体Size大小，需要重启IDE。
```

