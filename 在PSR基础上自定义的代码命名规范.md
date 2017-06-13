---
title: 在PSR基础上自定义的代码命名规范
date: 2017-03-30 22:52:24
tags: 面向对象
---

> PSR是PHP Standard Recommendations 的简写，由PHP FIG组织制定的PHP规范，是PHP 开发的实践标准。官网：https://psr.phphub.org 。

> 这篇文章是博主根据PSR基础规范和PHP100知名讲师张恩民的PHP教学视频进行整理，所有命名禁止使用阿拉伯数字。

<!-- more -->

### 目录、文件和局部变量

- 使用英文名词、动词，所有字母均使用小写，以下划线作为单词的分隔。
```
目录：upload,templates,install
文件：index.php,config.php
变量：$pay_time,$user_name,$article_del_time
```

### 全局常量

- 使用英文名词、动词，所有字母均使用大写，以下划线作为单词的分隔。
```
define('WEBSITE_NAME','erchoc');
define('WEBSITE_URL','http://www.erchoc.com');
```

### 数组变量

- 使用英文名词、动词，以下划线作为单词的分隔。
- 所有字母均使用小写，以_array结束。
```
$scopr_array = array();
$book_id_array = array();
```

### 对象变量

- 使用英文名词、动词，以下划线作为单词的分隔，可以完整采用类名或者简化类名，但是必须明确知道是什么类。
- 所有字母均使用小写，以_obj结束。
```
$user_obj = new userAccount();
$pay_obj = new payOrder();
```
### 类的命名

- 使用英文名词，以大写字母作为词的分隔，其他字母均使用小写。
- 名词的首个字母小写，类名不使用下划线。
```
class userAccount{......}
```

### 方法命名

- 使用英文名词、动词，所有字母均使用小写，以下划线作为单词的分隔。
- 对象属性的命名同理。
```
class userCar
{
  public $user_name = 'Erchoc';

  public function account_price_car()
  {
    ......
  }
  public function add_user_car()
  {
    ......
  }

}
```

### 函数、符号和运算符规范

- switch的每个case块都要换行再加上break，而default必须存在以处理特殊情况。
```
switch() {
  case 'user':
    ......
  break;
  case 'type':
    ......
  break;
  default:
    ......
  break;
}
```
- 声明定位风格：变量的代码块必须等于号对其，且初次使用变量必须初始化。
```
$tableName   = '';

$user_article = '';
```
- 尽量避免下面的做法：
```
$tableType;

$get_bookArticle = '';

$user_show = '';
```

### 其他基础规范

- 除书写SQL和需要加入变量的时候使用双引号，其他尽可能使用单引号代替双引号。

- PHP文件中尽可能不出现HTML语句，尤其是使用模板开发，考虑到模板兼容性，HTML文件中也尽可能减少PHP代码。

- 通常每个方法只完成一个特定的功能(逻辑动作事务)，所以方法的命名要能清楚说明它的用处，例如使用`email_error_check()`代替`email_chenk()`，用`pay_error_check()`代替`pay_chenk()`。

- 自定义方法和变量名不能与系统方法和变量冲突。

- HTML的form表单各元素的name和数据库字段名或者PHP接受变量一致，或者在字段名的基础上团队确定表单元素名添加前缀或者后缀。

- HTML的form表单不要采用缺省方法bool值判断非零数值，必须如下显式测试。
```
if($user_pay_num != false) {
   ......
}
```

### 各种注释的规范

- 流程控制和无参函数在实现前使用单行注释，需要特别说明的行在行尾添加单行跟踪注释。
```
//用户检测
if($check_obj->username( $username ) == true){
  ......
}

//获取用户信息
$user_name = $_POST['username'];
```
- 多参数方法注释：
```
/**
  *   分页预处理函数
  *  sql          SQL语句
  *  page         当前页数
  *  limit        每页现实的数量
  *  maxs         查询总数
  */
  function page_limit($sql, $page='0', $limit=10, $maxs='')
  {
    ......
  }
```

### 数据库设计与操作规范

- 数据库名称使用英文小写，以下划线分隔单词，以免跨平台时出现的大小写错误。

- 数据表名称应该由物体对象名称的小写字母组成，以下划线分隔单词。并尽可能对应系统中业务类的名称，如laravel框架的数据表名称为Model类的复数小写形式。

- 数据表的字段避免使用varchar和text等不定长的数据。

- 查询多表连接数据时候要求使用全名称或者别名，即使用`tableName.fieldName`代替`fieldName`。

- SQL语句应尽可能符合ANSI92标准，避免使用T-SQL或者PL-SQL等特定数据库对SQL语言的扩充特性。
