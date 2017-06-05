---
title: Laravel 5.4 Composer报错：指定的键名太长
date: 2017-05-12 23:51:50
tags: laravel
---

![图片来自简书](http://upload-images.jianshu.io/upload_images/3995745-9baacd89f2b04eee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> Laravel 5.4更改了默认数据库字符集，更改后默认使用的utf8mb4包括支持存储emojis。这只会影响新的应用程序，只要你运行的MySQL版本低于v5.7.7或者MariaDB低于10.2.2，就会碰到上述图片中的错误，那么我们该如何解决呢？

> laravel 5.4官方文档在数据库迁移(migrate)中给出了解决方法：编辑app/Providers/AppServiceProvider.php文件，并在boot方法中设置一个默认的字符串长度191即可：
key_to_long解决办法。那么你知道这样做的原理吗？

<!-- more -->

![图片来自简书](http://upload-images.jianshu.io/upload_images/3995745-cd5c87fb8b55afec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 实际上这个问题我们可以看看原理，以前的MySQL使用UTF8时候一个编码字符等于3个字节，那么varchar(255)字段的最大存储字节就是255*3=765。InnoDB给出的限制是767b，那么MySQL 5.7之前varchar这个类型就是可以正常使用的。

- 但现在默认的utf8mb4编码中一个编码字符为4个字节，那么最大的varchar类型的最大字节数就是2554=1020b，这已经远远超过了InnoDB给出现限制767b。由于1914=764<767，所以我们引入Schema类提供一个方法处理这个情况，通过boot方法调用了Schema的静态方法defaultStringLength设置所有varchar类型的字段的字符数默认(也是最大)为191。

- 实际上我在PhpStudy环境中只通过配置文件设置了MySQL默认数据库引擎为InnoDB就达到这一效果，这是因为我在低于MySQL5.7环境下新建voyager数据库时选择了utf8编码。
新建数据库时的字符集

![MySQL默认字符集问题](http://upload-images.jianshu.io/upload_images/3995745-c7d502cdb3d1c3ff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 当然，无论是开发还是线上环境，还是推荐使用官方提供的homestead环境，内置的PHP和数据库均为配套的最新版本，还有一大堆集成的可用工具。如果你使用Docker集成，也可以使用bug挺多尚不完美的LaraDock，开源地址：https://github.com/laradock/laradock。