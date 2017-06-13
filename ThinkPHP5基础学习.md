---
title: ThinkPHP5基础学习
date: 2017-05-30 01:38:47
tags: 面向对象
---

> ThinkPHP是伟大的中国人自己开发的一套php面向对象框架，最新的TP5改进很多方面并专注于钱后端分离的API开发，中文的注释，中文的文档，中文的社区都让中国中小规模的企业不得不选择这个框架。适合人员迭代和快速开发，一套约定的编码规范让团队协作更加清爽，内置的日志和调试器功能强大，直接就能查看到性能分析，支持composer组件化集成。

> 总之，很强，很有学习的必要！

<!-- more -->

### 一、获取ThinkPHP

- 获取ThinkPHP的方式很多，[官方网站](http://thinkphp.cn)是最好的下载和文档获取来源。建议使用composer或者git安装：
   - topthink/thinkphp是3.2版本。
   - topthink/think是最新thinkphp5。
   - topthink/framework是核心框架，一般不选择。

- 官网下载版本提供了完整版和核心版两个版本，核心版本只保留了核心类库和必须的文件，去掉了所有的扩展类库和驱动，支持标准模式和SAE模式，一般下载完整版进行开发。

---

### 二、环境要求

- 框架本身没有什么特别模块要求，具体的应用系统运行环境要求视开发所涉及的模块。ThinkPHP底层运行的内存消耗极低，而本身的文件大小也是轻量级的，因此不会出现空间和内存占用的瓶颈。

- PHP5.4以上版本（注意：PHP5.3dev版本和PHP6均不支持）。

- topthink/think依赖于php相应版本和topthink/framework组件。

- 支持Mysql、MsSQL、PgSQL、Sqlite、Oracle、Ibase、Mongo以及PDO等多种数据库和连接。

---

### 三、目录结构

- 下载ThinkPHP框架后，解压缩到web目录下面，可以看到初始的目录结构如下：

![ThinkPHP5.0.9目录结构](http://upload-images.jianshu.io/upload_images/3995745-c35d92bb6b6dfabd.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1440/q/50)

- 一级目录六个，分别是应用目录，拓展类库目录，web目录，运行时目录，框架系统目录，第三方类库。

- 一级目录中有一些文件，分别是协议，说明，composer配置和锁文件，think工具，自动生成定义文件build.php。

- README.md文件仅用于说明，实际部署的时候可以删除。

- 上面的目录结构和名称是可以改变的，这取决于你的入口文件和配置参数。

- ThinPHP默认路由访问顺序是/模块/控制器/控制器方法

---

### 四、入口文件

- ThinkPHP采用单一入口模式进行项目部署和访问，无论完成什么功能，一个应用都有一个统一（但不一定是唯一）的入口。应该说，所有应用都是从入口文件开始的，并且不同应用的入口文件是类似的。

 - 入口文件定义

 - 入口文件主要完成：

   - 定义框架路径、项目路径（可选）

   - 定义调试模式和应用模式（可选）

   - 定义系统相关常量（可选）

   - 载入框架入口文件（必须）

- 默认情况下，TP5版本的框架已经自带了一个应用入口文件（以及默认的目录结构），内容如下：

```
define('APP_PATH','./Application/');

require './ThinkPHP/ThinkPHP.php';
```
- 注意：3.2版本开始无需定义APP_NAME常量

- 如果你改变了项目目录（例如把Application更改为Apps），只需要在入口文件更改APP_PATH常量定义即可：

```
define('APP_PATH','./Apps/');

require './ThinkPHP/ThinkPHP.php';
```
- 注意：APP_PATH的定义支持相对路径和绝对路径，但必须以“/”结束

---

### 五、编码规范

- 使用ThinkPHP开发的过程中应该尽量遵循下列命名规范：

 - 类文件都是以.class.php为后缀（这里是指的ThinkPHP内部使用的类库文件，不代表外部加载的类库文件），使用驼峰法命名，并且首字母大写，例如 DbMysql.class.php；

 - 类的命名空间地址和所在的路径地址一致，例如 Home\Controller\UserController类所在的路径应该是 Application/Home/Controller/UserController.class.php；

 - 确保文件的命名和调用大小写一致，是由于在类Unix系统上面，对大小写是敏感的（而ThinkPHP在调试模式下面，即使在Windows平台也会严格检查大小写）；

 - 类名和文件名一致（包括上面说的大小写一致），例如 UserController类的文件命名是UserController.class.php， InfoModel类的文件名是InfoModel.class.php， 并且不同的类库的类命名有一定的规范；

 - 函数、配置文件等其他类库文件之外的一般是以.php为后缀（第三方引入的不做要求）；

 - 函数的命名使用小写字母和下划线的方式，例如 get_client_ip；

 - 方法的命名使用驼峰法，并且首字母小写或者使用下划线“_”，例如 getUserName，_parseType，通常下划线开头的方法属于私有方法；

 - 属性的命名使用驼峰法，并且首字母小写或者使用下划线“_”，例如 tableName、_instance，通常下划线开头的属性属于私有属性；

 - 以双下划线“__”打头的函数或方法作为魔法方法，例如 __call 和 __autoload；

 - 常量以大写字母和下划线命名，例如 HAS_ONE和 MANY_TO_MANY；

 - 配置参数以大写字母和下划线命名，例如HTML_CACHE_ON；

 - 语言变量以大写字母和下划线命名，例如MY_LANG，以下划线打头的语言变量通常用于系统语言变量，例如 _CLASS_NOT_EXIST_；

 - 对变量的命名没有强制的规范，可以根据团队规范来进行；

 - ThinkPHP的模板文件默认是以.html 为后缀（可以通过配置修改）；

 - 数据表和字段采用小写加下划线方式命名，并注意字段名不要以下划线开头，例如 think_user 表和 user_name字段是正确写法，类似 _username 这样的数据表字段可能会被过滤。

 - 特例：在ThinkPHP里面，有一个函数命名的特例，就是单字母大写函数，这类函数通常是某些操作的快捷定义，或者有特殊的作用。例如：A、D、S、L 方法等等，他们有着特殊的含义，后面会有所了解。

 - 由于ThinkPHP默认全部使用UTF-8编码，所以请确保你的程序文件采用UTF-8编码格式保存，并且去掉BOM信息头（去掉BOM头信息有很多方式，不同的编辑器都有设置方法，也可以用工具进行统一检测和处理），否则可能导致很多意想不到的问题。

### 六、开发建议

 - 在使用ThinkPHP进行开发的过程中，我们给出如下建议，会让你的开发变得更轻松：

   - 遵循框架的命名规范和目录规范；

   - 开发过程中尽量开启调试模式；

   - 多看看日志文件，查找隐患问题；

   - 养成使用I函数获取输入变量的好习惯；

   - 环境改变后首先要清空Runtime目录；

