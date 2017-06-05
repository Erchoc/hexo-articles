---
title: 新时代的composer组件化学习道路
date: 2017-06-02 08:34:22
tags: oop
---

> 自己搭建一个php的mvc框架，这个想法是我学CodeIgniter框架没几天就产生的想法，也确实去做了，可只是目录结构上有mvc的样子有什么用呢？写的代码没有一点面向对象的感觉，全是require引入文件。

> 使用composer搭建一个面向对象的组件化php框架，这个想法已经在我脑海中存在了好几个月。这个框架本打算暑假开始搭建，可最近心里老是想起这件事，于是今天早上5:37起床开电脑把开头的准备工作搞定了，其他composer组件添加并集成使用部分就慢慢搞好了，搞定路由下一个就是有点麻烦的Model数据库操作了。

<!-- more -->

#### 进度汇报

- 首先是composer项目的初始化我没有用使用composer init，而且通过composer.json开始项目。然后新建app框架应用目录，config项目配置目录，public前端访问目录，framework自定义类库。接着立刻开始github寻找合适了composer路由组件，考虑到初步学习就找了个加注释仅有163行代码的Macaw。然后前端建立index.php引入composer自动加载文件和config/routes.php路由配置文件，并在routes.php中使用Macaw调用不存在的静态方法get，第一个参数'/index'，在闭包函数中输出字符串。

- 这个时候通过修改hosts和vhost.conf将qframe.dev映射到本地public目录，我这里使用的是apache。访问该虚拟域名/index发现并没有成功输出字符串，但是访问index.php/index 却可以。这是因为apache的rewrite module开启后还需要书写.htaccess请求转发文件，这个步骤是apache伪静态的内容，我就直接把laravel的这个文件cp过来用了。

- 这时候用postman测试restful常用四大方法都没问题，路由部分就结束了。开始控制器和路由的关联。在app中新建Controllers并书写基础控制器和测试控制器，路由和控制器中的写法和laravel使用的写法类似，再次访问网址直接看不到界面了，这是因为composer.json没有加入自动加载配置。添加autoload键值对并使用classmap数组加载控制器目录，然后执行dump-composer更新锁文件即可。

- 接下来进入一个本可以很麻烦的阶段:数据库操作。由于RESTful以资源实体为目标，我将Model修改为具体的Entities，也方便后期分层添加Model层的其他处理目录。暂时我只能在控制器中连接数据库进行CURD操作，后期再来依赖注入。那么我们新建数据库，数据表，插入数据，然后在Entities中建立Article.php文章实体，composer.json的classmap数组加载该目录。

- 在Article的first静态方法中连接数据库并返回查询到的数据，在控制器中直接Article::first()即可。关于为什么使用静态方法，这一点我认为是防止后续还需要这段数据，减少查库操作。

#### 阶段疑问

- .htaccess书写用到了正则表达式且涉及到apache模块的开发和使用问题，存在少许疑问。

- Macaw.php一共就163行代码，暂时没有完全理解使用原因。

- 关于composer的autoload四种方式不太理解，以及spr-0在此处的兼容性使用。

- 关于数据库部分的配置和CURD操作封装问题，还需要学习一种composer组件，刚开始就不考虑这件事吧。

- 关于静态方法在此处使用的原因，不知道自己的理解有哪里不妥当和不完善之处。