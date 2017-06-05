---
title: Laravel 远程工作之开始前的准备和沟通
date: 2017-05-013 16:11:24
tags: laravel
---

> 前段时间在laravel-china社区的远程工作模块留言希望得到锻炼，结果没几周微信就有人加我询问情况。当时还在上课，又正好碰上S6 G9200刷机事件，直到晚上快十一点才电话联系上。

> 电话里对方简单问了下我学习php和laravel的情况，我做了个简单回复：php学习了一年，简单做过的企业站，laravel方面跟着慕课网完成了博客系统的后端api开发，没使用RESTful API，会用Git和Composer。对方也明确表示这是一个租赁系统，开发周期1-2月，询问我的业余时间段后给我开的价格是2K/m。本着学习的意愿我当然是同意了。

<!-- more -->

- 其实这个时候我学习上已经很忙了，并且处在穰学长的firechat微信项目开发优惠券模块中。考虑到学长并不是专门搞PHP，这个项目做的流程并不正规搞得自己也晕头转向的，想想laravel社区这位大牛和我说话时也表示会教很多东西给我们，正好用来补救firechat项目，同时也把学长这个项目学到的用在租赁系统的模块开发上，做的好还能额外拿到2K-3K呢。

- 两三周过后，这位大牛(以后简称晓乐)联系我说明老板和他们那边都准备好了，我们开始聊开发前的一些准备工作。本地环境要求有Composer和Git，我使用的PhpStudy集成环境PHP版本7.0，这个租赁系统基于laravel 5.1开发。心想幸好不是最新的5.4，否则数据库问题(见Laravel 5.4 composer报错：指定的键太长)又是一大尴尬，那我可能就要使用自己不太熟悉的homestead或者laradock了。

- 晓乐继续询问我是否对Git的分支管理有了解？这里听了郭佳栋的，都说不会总不会错。于是他给了我这个地址：http://www.ruanyifeng.com/blog/2012/07/git.html 。阮一峰大神的Git分支管理策略。代码放在他们公司搭建的Gitlab上，还给我创建了一个账号，说明了平时主要在dev上面开发，commit时候字数不要太多，尽量使用英文，要了解gitignore的作用，不要随意添加库文件等等。

- 然后就是团队协作软件了。以前刚接触laravel-china时候看到个小蜜圈觉得挺好的团队交流和协作开发工具，他这里使用的teambition却明显更加正规。我用手机注册账号之后他拉我进了名为租书的项目团队，说好下午拉我进入开发群。这次我学乖了，不敢多说话，等进群了也尽量少说话，免得人家把我当作菜鸟。其实我多问问学习也没错啊。

- 晓乐叫我下午把本地环境部署好，我想了想自己还是应该先把Git分支管理策略看一下，再登陆一下对方的gitlab看看，然后花点时间了解下teambition的基本使用，接下来搭建本地环境，看看这个项目进行到哪里了，目录和路由，引入了那些库等等。

> 下面是下午的操作：

- 下载并登陆Teambition客户端，修改了个人信息，下载并查看了小叮租书项目文件中的说明，数据库ER图

- 登陆私有Gitlab，修改了个人信息和密码，查看项目成员只有三个，另外两个都是领导。项目代码开始是william一周前提交上去的，另外提交的两次添加了zizaco/entrust和dingo/api两个第三方库，最近的一次添加了.gitignore中PhpStorm生成的.idea配置文件夹。

- 参考简书生成本地SSH密钥一文，搞定本地SSH和Gitlab，GitHub部署SSH。windows步骤如下：

```
查看用户目录下是否有.ssh文件夹 cd && ls -al

如果有，则执行删除目录命令 rm -rf .ssh

使用Git Bash执行 ssh-keygen -t rsa -C "your_email@example.com"

然后三次回车即可，不要自己添加这里没用的密码。

查看.ssh目录下的文件有  id_rsa id_rsa.pub known_hosts。
```

- SSH使用的非对称加密算法存在公钥和私钥的说法，私钥id_rsa保留在本地即可，我们需要往Github和Gitlab部署的是公钥id_rsa.pub中的所有字符串。[点击查看非对称加密详情](https://my.oschina.net/realfighter/blog/388486)。

- cat id_rsa.pub输出文件内容复制后打开github网站。

- 粘贴到Github的Settings》SSH and GPG keys和Gitlab的Profile Settings》SSH Keys即可，命名随意，需要验证密码。

- 下载项目源码本地部署，项目用到的composer包如图。

- 后台用到的composer包

![图片来自简书](http://upload-images.jianshu.io/upload_images/3995745-b249a97abdac8292.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
git clone http://gitlab.develop.umeishu.com:port/root/rent-api.git 。

由于魏关闭了服务器22端口，无法使用ssh下载。但是公钥部署和Access Token依然有用。

git checkout -b develop master

这里是是分支管理的内容，创建并切换到开发分支。

cp .env.example .env

新建rent数据库,切换win10的bash执行，修改.env中数据库和登陆账号密码。

php artisan key:generate

生成项目唯一key值。

修改本地hosts,添加rent.dev映射，配置phpStudy虚拟域名，访问rent.dev测试。
```
- 由于我clone的master，remote上的dev版本比master新。所以我要pull拉一下服务器上的dev代码，使用git pull origin dev，dev是服务器上分支名称，pull之后本地代码就会有变动，Route就会添加。

- 然后compoer install更新一下依赖包，访问测试路由/hello 出现一个错误：

```
Unable to boot ApiServiceProvider, configure an API domain or prefix
```

- 这是因为remote的dev上使用了用于RESTful API的dingo/api包，我pull的时候.env.example文件添加了几个API开头的配置项。全部复制到.env中并且将API_DOMAIN配置为本地映射的虚拟域名即可，再次访问/hello 搭建成功。
