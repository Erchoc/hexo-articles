---
title: 第N次安装Hexo框架和Next博客主题
date: 2017-06-01 08:14:10
tags: 技术博客
---

> 换了 Mac 之后 Hexo 框架和主题文章全没了，备份到码云的文章数据被 .gitignore 忽略了，没办法找个时间自己手动备份一下 Hexo 博客。这次懂事了，必须用iCloud把数据全备份下来，这里 windows 下的 OneDrive 即时备份机制真恶心。

> 然后就是`npm install -g hexo-cli`安装 hexo 客户端工具，在 ~/Documents/Hexo/ 目录下初始化框架：`hexo init`。这些操作在第一篇文章`又写Next博客`就提过，这里又说了一遍。为了表示差异性，这篇文章我就主要讲一些功能特效和 Next 主题的配置吧。

<!-- more -->

- Next三种主题选择

> 在配置文件中搜索 Schemes ，你会看到`Muse, Mist, Pisces`三种 scheme，去掉你喜欢的主题前的 # 注释即可。修改主题需要重启 hexo 服务并执行清除缓存操作：`hexo clean`。

- 右下角的屏幕滚动百分比设置。

> 配置文件中将 scrollpercent 设置为 true 即可，如果你要让百分比在侧边栏显示，只需要把b2t的值也设置为 true。

- 多种canvas背景特效

> 在配置文件中选择性的把 canvas_ 开头的值设置为 true 即可，特效可以同时设置为 true。

- 关闭被墙的 Google 字体

> 配置文件中将 font 中的 enable 和 global 中的 external 设置为 false 即可。

- 给博文添加协议

> 配置文件中把 post\_copyright 的 enable 设置为 true 即可，如果你想在侧边栏也有这样的提示图标，把 creative_commons 的值设置为 by-nc-sa 即可。

- 前端/本地搜索功能

> 配置文件中的 local_search 中将 enable 的值设置为 true 即可。

- 友情链接 /social links 设置

> 打开配置文件中 social 的默认注释并添加链接即可，例如: `简书博客: http://www.jianshu.com/u/9d64b43bc1a1`。同时可以为友情链接设置 FontWaesome 图标，图标名参考 FontAwesome 官网：http://fontawesome.io/icons

- 博主头像设置

> 在 next/images/ 中放入你的头像，名称为 avatar.jpg ，然后打开 Next 配置文件`Sidebar Avatar`中avatar默认的注释并修改对应的值为`/images/avatar.jpg`，你也可以根据这里的说明把头像放倒 uploads 文件夹下。

- 网站图标设置

> 将图片转换为图标，将图标文件 favicon.ico 放到 next/source/ 目录下，然后在 next 配置文件中搜索并修改 facicon 的值为`/favicon.ico`。

- 代码高亮主题

> Next 有五款使用了Tomorrow Theme的代码高亮主题，在配置文件中修改 highlight_theme 的值即可。文章使用(```)的代码段将会采用这种主题配色。

- 开启微信/支付宝打赏功能

> 首先确保 layout/_macro/ 目录下存在 post.swig 和 reward.swig 两个文件，缺少则以utf-8为编码新建这两个文件，并点击[这个地址](https://github.com/iissnan/hexo-theme-next/blob/master/layout/_macro/reward.swig)中的代码复制粘贴到新建的文件中。然后再配置文件中的任意位置添加如下几行代码：

```
# 增加Donate 打赏功能
alipay: /uploads/alipay.png
wechatpay: /uploads/wechatpay.png
reward_comment: 坚持原创技术分享，您的支持将鼓励我继续创作!
```
> 注意事项：微信和支付宝提供的图片格式不一样，尺寸也不同。

>上述操作我目前是失败了请求各位道友指点。

- 订阅微信公众号

> Next 5.0.1版本加入该功能，在每篇文章末尾显示公众号二维码。你只需要将公众号二维码 wechat-qcode.jpg 从微信平台下载后放在 source/uploads/ 目录下，然后将配置文件中的 wechat_subscriber 的enable 值设置为 true，qcode 设置为 /uploads/wechat-qcode.jpg，descripion 值设置为 `欢迎您扫一扫上面的二维码，关注技术博客最新动态`。

- 用户评论系统

>

- 自定义导航栏

> 打开 menu 中的注释再访问网址，你会发现网页提示`Cannot GET /categories/`，你需要

- 自定义导航栏之文章分类

>

- 自定义导航栏之关于博主

>

- 网站404页面设置

> 在 /source/ 目录下心间 404.html 页面，内容随你开心填写，建议使用下面腾讯公益404儿童丢失页面：http://theme-next.iissnan.com/theme-settings.html#volunteer-404

- 自定义导航栏之标签管理

>

