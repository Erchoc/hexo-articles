---
title: 在MacOS上安装和使用Docker搭建laravel环境
date: 2017-05-20 01:25:54
tags: 高效工具
---

> 首先当然是下载docker, 推荐使用增强型brew`brew cask install docker`安装, 其实就是下载了这个文件, 你也可以自己下载这个文件然后进行手动安装: https://download.docker.com/mac/stable/17661/Docker.dmg 。

> 100MB出头, 下载要点时间。安装成功后我们开始使用`sudo docker version`命令行测试操作, 成功的标志是终端返回docker服务端和客户端版本信息, 另外请记住服务器上Docker的绝大多数命令都需要在root权限下执行。绝大多数你想的docker配置信息都可以使用`docker info`来查看。

<!-- more -->

![测试安装是否成功](http://upload-images.jianshu.io/upload_images/3995745-0501e24fc8597a82.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 由于Docker在2017年三月的大更新, 导致现在存在CE, EE和以前的Docker老版本, 如果直接使用yum, apt-get, brew install docker/docker.io/docker-io可能会下载到老版本。新版本要求linux内核大于3.8。

- 现在我们先cd到家目录, 使用composer创建个laravel程序:

```
composer create-project laravel/laravel example
```

- 当然你也可以选择使用git手动创建修改配置文件

```
git clone https://www.github.com/laravel/laravel.git
```

- 但是composer创建的好处在于它会自动帮你生成.env配置文件和加密key, 还会自动执行composer install下载依赖(下载慢的话请配置过程compsoer全量镜像)。

- 下载完了我们进入这个目录并使用php命令创建内置的测试服务器:

```
cd && sudo php -S localhost:8080 -t ./public
```

- 然后访问localhost:8080, 显示laravel主页则关闭php内置服务器, 开始使用dockerfile。(这一步骤使用php命令可能需要管理员权限, 使用php artisan serve不需要管理员权限)

- 我们首先在下载laradock这个写好dockerfile的一个文件夹:

```
git clone https://www.github.com/laradock/laradock.git
```

- laradock的官方文档在[这里查看](http://laradock.io), 但是很多使用讲解不清楚, 出现问题建议查看github源码托管所的Issues, windwos用户使用就是各种坑：

```
启动mysql容器会报错, 那是因为windows的文件目录结构和Unix是不同的。

你需要在配置文件中修改本地mysql数据保存路径，默认的路径写法是类unix的。

win下模拟终端环境把盘符挂在/mnt目录下, 没有真正的超级管理员权限, 使用docker会碰到权限问题。

内存不足问题, docker重启失败问题, mysql容器启动失败, apache配置文件错误等等一系列问题。

我前几天就是因为受不了这一点菜忍痛借钱买苹果电脑。
```

- 现在你的example和laradock都在~/目录, 那么进入laradock目录执行命令生成环境的配置文件：

```
cp env-example .env
```

- 修改.env文件中的一些配置信息：

```
DB_HOST=mysql,

REDIS_HOST=redis,

QUEUE_HOST=demo,
```
- (如果你的mysql安装在本机127.0.0.1就可以不需要修改这部分, 修改主要是方便上线在内网部署mysql服务器, 这样修改不需要指定内网mysql的ip地址)。

![Docker原理](http://upload-images.jianshu.io/upload_images/3995745-0c05d731f533ddfd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 如图Docker在pull一个可使用的镜像, 镜像是可读不可写的, 图中可见该镜像有七个添加后的可写层并被重新构建了images, 现在正在下载压缩镜像并解压镜像启动容器, 这个步骤容易出问题, 那就直接去github issues搜索相关问题。

- laradock目录下可以使用环境构建工具docker-compose启动容器, 例如启动mysql, apache, redis容器实例各一个:

```
docker-compose up -d mysql apache2 redis
```

- docker会查看你本地是否存在需要的镜像, 没有的话它就会自动根据dockerfile里面的代码起pull images, then build containers。

- 一般情况下php-fpm和workspace容器不需要指定就会被启动。

- 我们就可以进入workspace容器中使用里面的git, composer, npm, glup等一系列命令:

```
docker-compose exec workspace
```

- 其实每一个容器你都可以进去, 只是推荐进入这个为开发者打造的workspace而已, 你也可以添加参数指定以哪个用户进入(由于composer不推荐使用默认的root执行compsoer命令), 还可以指定端口, 可以指定进入时候使用何种shell, 我也不知道在Mac上是不是可以指定zsh。

- 默认从国外的docker官方hub下载镜像, 建议使用阿里云或者DaoCloud加速器。

```
点击Docker图标, Preferences, Daemon

将加速器链接添加到下方的镜像仓库中应用并重启即可。
```
- 你操作前后使用`docker info`可以查看到镜像仓库的改变。

- 当然, 其他平台如windows和linux也可以使用DaoIcoud官方提供的方法配置加速器:
https://www.daocloud.io/mirror#accelerator-doc。

> ![添加镜像加速服务](http://upload-images.jianshu.io/upload_images/3995745-edcf937bc41dbb81.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 查看一下容器启动情况, 你可以使用`docker ps`查看正在运行的所有容器。

- 也可以进入laradock目录只查看laradock中使用docker-compose启动的容器:

```
docker-composer ps
```

- 看到容器启动成功(和你使用`ps aux|grep nginx`类似, 容器启动成功后又一个容器是会关闭的, 没任何影响哦)后就访问localhost或者虚拟域名进行测试吧。

- 修改.env中的配置, 单个项目只需要改成  `APPLICATION=../example/`, 多个项目设置不需要改变这个配置文件。别down销毁容器，只能修改后重启Docker容器：

```
docker-compose restart
```

![成功结果](http://upload-images.jianshu.io/upload_images/3995745-3b02bcc177b4e454.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![部署完成](http://upload-images.jianshu.io/upload_images/3995745-36a98bfe7b291d5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 其他常用命令:
    - 停止所有容器运行
    `docker-compose stop`

    - 停止mysql容器运行
    `docker-compose stop {container name}`

    - 删除所有容器
    `docker-compose down`

    - 删除指定容器
    `docker-compose down {container name}`

    - 后台启动容器(本地没有镜像则会先pull)
    `docker-compose up -d {container name}`

    - 进入容器:
    `docker-compose exec {container name} bash/zsh`

    - 查看正在运行的容器
    `docker-compose ps`

    - 查看历史所有的容器
    `docker-compose ps -a`

    - 查看日志文件
    `docker logs {container name}`

    - 重建所有容器
    `docker-compose build`

    - 重建某个容器
    `docker-compose build {container name}`

    - 退出容器
    `exit`

- 关于虚拟域名配置, php版本切换, 安装XDebug, apache和nginx多站点和php拓展安装大家就看文档吧, 这部分挺简单的。

- laradock作为docker中的homestead稍微有些庞大, 并且使用laradock部署yii和普通的php项目不太合适, 所以我最近转向使用phpdocker.io, 这是一个可定制的dockerfil生成器, 并且简洁清爽, 缺点就是官方文档几乎没有。

- 自己对docker还有一些问题不太清楚, 关于dockerfile和持续集成部署也尚未实战了解, 希望这次能从晓乐这边学到很多东西。
