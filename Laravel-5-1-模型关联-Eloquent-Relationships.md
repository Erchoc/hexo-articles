---
title: Laravel 5.1 模型关联(Eloquent Relationships)
date: 2017-05-16 00:34:28
tags: laravel
---

> 项目的数据库部分昨晚晓乐已经微信视频和我讲了近一个小时，`小叮租书`项目的后台使用laravel开发接口和业务逻辑部分，前台部分是由海洋大学以为大二的前端学生在做。这个项目数据表很多，大体上分为了`product`,`order`和乱七八糟的`er-common`部分。

> 项目涉及到的实体比较多，昨天另一个PHPer把数据表全部migration写完push上去了，担心我不会今天的API-Model怎么写，晓乐还特意写了Role和Permission部分。然后，我也确实不会写，一开始都不知道到底要写啥，等讲完一小时的数据表才知道：**原来是要我写模型里面实体间的对应关系**。

<!-- more -->

- 没办法咯，看官方的英文文档的Eloquent: Relationships部分咯。文档指出实体之间的关系有七种(六种：一对多和多对一可以理解为一种)：

```
一对一
一对多
多对一
多对多
远程一对多
多态关联
多态多对多关联
```

- 使用模型关联之前，我们要先定义每个实体关系的类型。

- 首先创建一个继承了Eloquent/Model类的User Model，根据项目ER图找出和用户实体有关系的实体：

  - `role角色`，`permission权限`，`school学校`

  - `enrollmentInfo学籍`，`orders订单`，`coupons优惠券`

  - `addresses地址`，`carts购物车`

- 除了和实体的关系，User Model还应该定义一些用于获取id，token信息的函数。

- 为啥上面的实体一些是单数一些是复数呢？这就是laravel所谓的约定大于配置。用户和其他实体之间的关系决定了User类中关系函数的单复数形式。比如说用户和订单的关系，一个用户可以下多个订单，一个订单之恩那个属于一个用户，所以他们之间是一对多的关系，使用Eloquent内置的hasMany函数表明相对关联：
```
public function orders()
{
      return $this->hasMany('App\Entities\Order');
}
```

- 那么现在的重点就是两个：表明相对关联的Eloquent内置函数有哪些？请看https://cs.laravel-china.org/#eloquent 。千万不要和Laravel内置的辅助函数(帮助函数，助手函数，Helpers函数)搞混哦，简单用法如下。
```
// 一对一 - User::phone()
 return $this->hasOne('App\Phone', 'foreign_key', 'local_key');
// 一对一 - Phone::user(), 定义相对的关联
 return $this->belongsTo('App\User', 'foreign_key', 'other_key');

// 一对多 - Post::comments()
 return $this->hasMany('App\Comment', 'foreign_key', 'local_key');
//  一对多 - Comment::post()
 return $this->belongsTo('App\Post', 'foreign_key', 'other_key');

// 多对多 - User::roles();
 return $this->belongsToMany('App\Role', 'user_roles', 'user_id', 'role_id');
// 多对多 - Role::users();
 return $this->belongsToMany('App\User');
// 多对多 - Retrieving Intermediate Table Columns
$role->pivot->created_at;
// 多对多 - 中间表字段
 return $this->belongsToMany('App\Role')->withPivot('column1', 'column2');
// 多对多 - 自动维护 created_at 和 updated_at 时间戳
 return $this->belongsToMany('App\Role')->withTimestamps();
```

- 那么回过头来看看这个项目中app/ Entities/目录下那么多个实体Model(Entities就是个目录，改成Model也行，但是Entities翻译过来就是更准确的`实体`的意思，我一开始还以为是啥厉害的Composer包呢)。我们看看User.php和上面说的有啥不同。
![首先](http://upload-images.jianshu.io/upload_images/3995745-d20d4c221ba4aee0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 首先命名空间和使用缓存，然后是Eloquent的软删除(也叫softdelete,惰性删除，要和惰性加载load区分一下)。其他的四个是用来认证授权的一些内容，这个项目的认证授权使用第三方包JWT，有空我得了解一下。

- 然后就是User Model实现接口AuthenticatableContract和AuthorizableContract(其实我也不太清楚这接口在哪里定义的，为什么要这样写)，接着开始定义一些配置，比如:

```
  1. 表名不是默认的名词+s形式，则需要指定$table。

  2. 如果表中不存在created_at和updated_at，需要将timestamp指定为false，即关闭自动维护时间戳。

  3. 按照情况添加guarded数组，如created_at等。

  4. 如果存在deleted_at，为model添加softdelete 的trait。(写文章时候这一点我还不理解)

  5. 对于外键不是【表名单数】_id这样形式的，需要在指定关系时，显性指定键名，如address表中的province_id指向areas，就需要单独指定。
```

- 对比项目User.php和上面的函数你会发现hasOne()还能带参数，也是定义配置里面的重新定义外键，因为默认情况下外键名称是基于Model名称的。包括第三个参数，具体请看：http://d.laravel-china.org/docs/5.1/eloquent-relationships 。

- 除此之外这个文件中海油获取user_id的getAuthIdentifier()，获取user_password的getAuthPassword()和静态的addUser()。

- 实际上这个部分不仅仅写模型关联这么简单，还有获取数据，更新删除数据的方法，Model相关的内容包括

  - `基础用法`，`更多用法`，`软删除`，`模型关联`，`事件`和`Eloquent配置信息`。

- 那么我就联系了另一个工作三年的PHPer，问下他写了哪些实体关系，我就开始写咯，要写的如下：
```
Account  账户
Address  地址
Cart  购物车
Category  分类
College  大学
Coupon  优惠券
EnrollmentInfo  学籍信息
EnrollmentUnit  学籍单位
Entity  相当于Eloquent/Model，这里所有实体的父类
Inventory  库存
Item  商品
Major  学生主修专业
Order  订单
OrderAddition  订单辅表
OrderHistory  历史订单
OrderItem  订单商品表
Payment  付款方式
PaymentRecord  付款记录
Permission  权限，william wei写完了。
    - 多对多roles
Product  产品
ProductAttr  产品属性
ProductAttrValue  产品属性值
Role  角色，william wei写完了。
    - 多对多users，多对多permissions
School  学校
Shipping  配送方式
StockOutRecord 出库记录
Tag  标签
User  用户，william wei写完了。
    - 一对多school，一对一EnrollmentInfo，多对多Role，
    - 一对多orders，多对多coupons，一对多addresses，一对多carts
Warehourse  仓库
```

- 注意，一对多和多对一概念类似但是函数名单复数不一致哦。学生对学校是一对多，使用school()；学校对学生是多多对一，使用students()。

- 使用belongsTo时可能是一对一，也可能是一对多。

- 上面有少数是实体之间的联系表，考虑到适度增加冗余于是给该表增加字段作为实体操作，例如：product。

- 怎么查看本地和远程代码的区别呢，使用`git diff`命令咯(zsh下默认别用gd)，但是需要自己指定参数哦，常见参数有：
```
git diff test 查看本地当前分支与本地test分支的区别

git diff dev master 查看本地dev分支与远程master分支的区别

git diff pull test 查看下次提交到远程dev分支时出变化的内容
```

> 这个部分git命令没写好以后继续添加，并追加到以前的Git命令学习文章中。另外下篇文章就是我单独把上面所有实体关联写完的烧脑过程，对着ER图一直想，一个XXX可以有YYY个ZZZ，但是一个ZZZ只能有YYY个个XXX，所以这个N对M模型，然后对照速查表写关联函数。