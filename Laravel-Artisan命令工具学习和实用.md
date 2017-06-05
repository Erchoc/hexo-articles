---
title: Laravel Artisan命令工具学习和实用
date: 2017-03-17 23:40:53
tags: laravel
---

> 本文以laravel5.4为例,建议刚开始学习Laravel框架的朋友先不使用Artisan进行项目开发。而是手动新建文件书写重复代码了解加载顺序，熟悉之后使用Artisan瞬间提高十倍工作效率。

<!-- more -->

### 简介

- Artisan 是 Laravel 内置的命令行接口。它提供了一些有用的命令协助您开发，它是由强大的 Symfony Console 组件所驱动。利用它，我们可以快速的新建Controller、Model等类。

- 查看所有artisan命令
> php artisan (list)

- 查看命令帮助信息
> php artisan help migrate

- 创建控制器
> php artisan make:controller UserController

- 创建Eloquent 模型类：
> php artisan make:model User

### 更多用法

| 命令 | 解释 |
| ------------- |:-------------:|
| php artisan list | 查看所有可以使用的 Artisan 命令 |
| php artisan help migrate | 浏览命令的帮助 |
| php artisan --version | 显示目前的 Laravel 版本 |
| php artisan down | 进入维护模式 |
| php artisan up | 退出维护模式 |
| php artisan make:provider name | 创建一个新的服务提供者类 |
| php artisan make:request name | 创建一个新的表单请求类 |
| php artisan migrate | 进行数据库迁移（名称：migration）|
| php artisan make:migration create_article_table | 创建article表结构 |

- 生成模型文件和迁移文件：
> php artisan make:model Article
> php artisan make:migration create_articles_table

- 建议创建migration迁移文件时追加--create=articles参数，这样会使新的迁移文件添加默认格式。

- 在database\migrations目录生成了2016_09_10_020228_create_article_table.php。该文件只有迁移前编写的up
方法和删除或者覆盖数据表使用回滚时的down方法，我们只需修改up方法：

- Laravel中Model对应的表名是其英文单词的复数形式(内部使用了英文词语的单复数映射)，例如UserModel在数据库中的体现就是users表。接下来让我们把 PHP 代码变成真实的 MySQL 中的数据表，运行命令：
> php artisan migrate

- 执行成功后，articles 表已经出现在数据库里了。articles里字段名可以改为你想要的名字，建议统一命名。

- 完成后数据库里还会多了个migrations表，用来记录数据库迁移信息，并且database/migrations/目录下记录着采用RoR思想诞生的迁移文件，这些文件不允许删除，否则不利于交付和迭代。

### Seeder使用

- database/seeds/下则对应相应的数据库改动信息，包含数据。

- Seeder 解决的是我们在开发 web 应用的时候，需要手动向数据库中填入假数据的繁琐低效问题。运行以下命令创建 Seeder 文件：
> php artisan make:seeder ArticleSeeder

- 我们会发现database/seeds/里多了一个文件 ArticleSeeder.php，修改此文件中的 run 函数为：
```
public function run() {
    DB::table('articles')->delete();
    for ($i=0; $i < 10; $i++) {
        \App\Article::create([ 'title' => 'Title '.$i, 'body' => 'Body '
        'user_id' => 1, ]);
    }
}
```

- 上面代码中的 \App\Article 为`命名空间绝对引用`。

- 接下来我们把ArticleSeeder注册到系统内。修改database/seeds/DatabaseSeeder.php
中的 run 函数为：
```
public function run() {
    $this->call(ArticleSeeder::class);
}
```
- 由于database目录没有像app 目录那样被composer注册为psr-4自动加载，采用的是psr-0 classmap方式，所以我们还需要运行以下命令把ArticleSeeder.php加入自动加载系统，避免找不到类的错误：
> composer dump-autoload

- 然后执行 seed：
> php artisan db:seedSeeded: ArticleSeeder

- 这时候刷新一下数据库中的 articles 表，会发现已经被插入了 10 行假数据。

### 参考：

- 1、Laravel 5.1 LTS 速查表
 [https://cs.phphub.org/#artisan](https://cs.phphub.org/#artisan)

- 2、Laravel 5.0 中文文档：Artisan 命令行接口
[http://laravel-china.org/docs/5.0/artisan](http://laravel-china.org/docs/5.0/artisan)

- 3、2016 版 Laravel 系列入门教程（一）
[https://github.com/johnlui/Learn-Laravel-5/issues/4](https://github.com/johnlui/Learn-Laravel-5/issues/4)