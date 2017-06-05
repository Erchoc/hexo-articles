---
title: Blade模板引擎入门问答学习
date: 2017-03-22 22:52:42
tags: laravel
---

> blade是laravel框架默认使用的模板引擎，这篇文章讲解blade模板的写法和完全指南。

<!-- more -->

- 怎么在模板引擎输出变量？
```
首先路由转发到一个控制器的一个方法，然后返回视图，同时使用链式操作with()方法，第一个字符串参数为模板变量，第二个字符串参数为实际的数据，然后模板文件输出即可。

当然，你也可以在控制器方法内部先声明或者得到一个$data数组，这也是开发常用的做法，只是获取$data的操作由model去完成并返回。
```

- 参数分别有数组和字符串，怎么办？
```
在view()方法中使用compact()方法把不同类型的数据传递到模板，然后在模板文件中分别输出数组和字符串(compact方法的变量参数不需要$符号)，

模板中输出可以使用嵌套php，也可以使用双大括号。
```

- 双大括号和Angular的语法冲突怎么办？
```
要么修改Angular定界符，要么Blade输出前加@符号。
```

- 查询文章，文章为空时候显示null？
```
模板引擎设置默认值{{ $name or '默认值' }}
```

























---

### Blade的六大流程控制语句

- 模板引擎的流程控制 if 怎么写？？？
```
     @if($persion['score']<0 ||$persion['score']>100)
       不合法
     @elseif($persion['score']<60)
       不及格
     @else
       及格
     @endif

如果传递的参数为字符串，模板引擎会转换为数字进行比较。
```

- 模板引擎的流程控制 unless 怎么写？
```
     @unless($persion['score']>=60)
       不及格
     @endunless

除非大于60分，否则都输出不及格，相当于 if !。
```

- 模板引擎的流程控制 for 怎么写？
```
    @for($i=0; $i<=$persion['score']; $i++ )
      {{$i}}<br />
    @endfor

for是可以嵌套使用的哦。
```

- 模板引擎的流程控制 foreach 怎么写？
```
    @foreach($persion['article'] as $v)
      {{ $v }}
    @endforeach
```

- 模板引擎的流程控制 forelse 怎么写？？？
```
    @forelse($persion['news'] as $v)
      {{ $v }}
    @empty
      没有数据
    @endforelse

for else是对foreach的补充，要求填写没有数据时候的默认显示文字，一般可用来替代foreach。
```

- 模板引擎的流程控制 while 怎么写？？？
```
    @while(3>1)
      {{ $persion['score'] }}
    @endwhile

你可以试试。
```
- 来个多种嵌套例子吧？？
```
    @forelse($persion['article'] as $k => $v)
      @if($k>2)
        {{ $k }}->{{ $v }}<br />
      @endif
    @empty
      没有数据
    @endforelse
```

---

- 公共模板替换

- 怎么添加公共头部尾部呢？
```
    @include(common/header)
    @include(common/footer)
```

- 怎么添加略有不同的公共头部尾部呢？
```
    @include('common/header', ['page' => '首页'])
    @include('common/header', ['page' => '文章页'])
    {{ $page }}

那当然是要传递参数啦！公共页面使用双大括号接受并输出参数字符串。
```

- layouts布局具体怎么实现流程是什么样的呢？
```

这个还是让我先想想怎么说吧。。。
```
