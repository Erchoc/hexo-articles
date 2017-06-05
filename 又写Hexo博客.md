---
title: 又写Hexo博客
date: 2017-05-07 16:06:53
tags: hexo
---

> 本来是真的不太想再整博客这东西，特别是github免费的空间配合hexo框架整的真烦，可是很多知识不记录又容易忘记，不写博客又显得自己没有竞争力，想想还是硬着头皮上了github上Hexo框架领域star数第一的next主题，这里真的不得不吐槽Hexo框架的报错合Debug策略。其实原来也挺喜欢一位学长使用的漂亮主题yilia，前端内容笔记也很翔实，https://hzzly.github.io 。我也会尽量同步简书和本站内容，目前只能手动同步，各位有啥好办法可以邮件或者文章留言留言联系我。邮箱：erchoc@qq.com。

> 阅读全文,开始配置Hexo+Next吧，Coding Notes Start.

<!-- more -->

- 运行下面的命令确保你安装了node/npm和git，git需要配置提交代码时用于区别用户的全局个人信息。

```
npm –version && git –version
```

- 全局安装hexo框架的客户端构建工具hexo-cli

```
npm install hexo-cli -g
```

- 新建并进入项目文件夹

```
cd && mkdir Hexo && cd Hexo
```

- 初始化hexo框架项目，自动安装框架代码和一个默认主题landscape

```
hexo init
```

- hexo框架默认目录结构

```
_config.yml   站点全局配置
package.json  npm包和依赖管理
scaffolds     模板文件夹
source        源文件
└── _posts    文件markdown源码
themes        主题,默认有landscape
```

- 启动Hexo内置服务器默认的4000端口查看博客是否搭建成功

```
hexo serve 或者 hexo s
```

- 下载主题并在正确目录放置

```
git clone https://github.com/iissnan/hexo-theme-next ~/Hexo/themes/next
```

- 修改_config.yml中应用的主题为next,重新hexo s查看浏览器

- 安装git部署模块hexp-deployer-git

```
cd ~/Hexo && npm install hexo-deployer-git -–save
```

- 生成public下的静态文件

```
hexo generate 或者 hexo g
```

- 清除生成的静态文件和缓存数据

```
hexo clean
```

- 在hexo的配置文件中设置deploy自动部署信息

```
type: git
repo: https://github.com/Erchoc/erchoc.github.io
```

- 演示部署到github

```
hexo deploy 或者 hexo d
```

- 其他注意事项

```
hexo s本地测试失败原因基本是因为配置文件填写错误,clone官方的配置文件替换即可。

hexo+next静态博客在windows这种系统上更新操作容易丢失数据，建议云盘备份source目录。

```