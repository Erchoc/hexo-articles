---
title: BootStrap3入门学习(样式篇)
date: 2017-03-25 10:42:31
tags:
---

> 教程整理自慕课网(原文部分错误在这篇文章得到修改，本文版本Bootstrap3.3.7)。文章有上下两个篇幅，分别是BootStrap3在样式和JS特效果组件的学习和说明。这篇文章是上半部分样式篇章。

<!-- more -->

### 框架简介

- Bootstrap是个前端UI框架，由Twitter两位员工写了这个框架后开源到github上。作为前端UI框架，你还可以使用jquery ui,Bourbon和轻量级的Pure.css。bootstrap每次版本更新变化都比较大，并且版本之间很多语法类名都不兼容，目前已经出了v4版本，但线上主要都在使用v3版本，v2版本早就被放弃维护。

### 目录说明

- Bootstrap3的dist文件夹中需要的只有三个可被引用的文件，bootstrap.css,bootstrap.js和theme.css，其他还有对应的压缩版和编译生成的.map文件。

- 主题文件就是矢量图标库，bootstrap有第三方矢量图标厂商为其免费提供使用，在Bootstrap4中已经没有这个文件，官方建议开发者自行下载引入awesome的矢量图标。

- 另外在bootstrap3中是使用了重置样式中最出名的normalize.css，bootstrap4却加入了reset.css文件，在normalize.css的基础上加入了自己的见解。

- 激进的bootstrap4放弃了对IE9以下的支持，其实也就是懒得引入加载那么多用于兼容的JavaScript文件了,即使是Bootstrap3,如果你不引入兼容文件，IE678依然对CSS3的支持很差。

- 大多数人只是用Bootstrap的样式布局，也有人使用其封装好的JS组件，在那之前你应该引入对应版本的jQuery文件。对于类似360这种双核国产浏览器，应该加入meta强制使用webkit内核渲染。对于IE用户，应该加入meta强制使用最新渲染模式。

### 关于Bootstrap3的六个标题

|元素|字体大小|计算比例|其他样式|
|:----:|:--------:|:---------:|:----------:|
|h1|36px|14px*2.60|margin-top:20px|
|h2|30px|14px*2.15|margin-bottom:10px|
|h3|24px|14px*1.70|.|
|h4|18px|14px*1.25|margin-top:10px|
|h5|14px|14px*1.00|margin-bottom:10px|
|h6|12px|14px*0.85|.|

- 所有标题的行高都是font-size的1.1倍，且文本颜色和字体都是继承父元素。

- 在标题标签内部使用<small-标签制作副标题，副标题默认不加粗字体颜色#999，h1-h3中的副标题字体大小为65%，h4-h6中的副标题字体大小为75%。

### 关于正文段落的p标签

- 由于全局字体大小为14px，段落行高是14*1.4285大概为20px，这个倍数是编译算出来的。

- 段落默认颜色为#333深灰色。字体为Helvetica Neue优先，对中文不友好可以手动修改。

- 段落默认距上下有10px的外边距。

### 强调内容

- 添加.lead类强调内容，其效果是
```
margin-bottom: 20px;
line-height:1.4;
font-size: 16px;
font-weight:300px;
```
- 但是在min-width: 768px的情况下它的字体大小为21px;

- 此外你也可以使用b，strong加粗。使用em，i或者CSS的font-style: italic使字体倾斜。

### 强调相关的六个类

- 类似于lead，Bootstrap还有六个强调类名用于表示文本颜色：

|强调类名|字体颜色|十六进制|
|:---------:|:---------:|:---------:|
|text-muted| 浅灰色 |   #777   |
|text-primary| 蓝色  |#337ab7|
|text-success|浅绿色|#3c763d|
|text-info  |  浅蓝色  |#31708f |
|text-warning| 黄色 |#8a6d3b|
|text-danger   | 褐色 |#a94442|

### 文本对齐风格

|  对齐方式  |  对齐类名  |
|:-----------:|:------------:|
|  左侧对齐  |  text-left   |
|  右侧对齐  | text-right |
| 居中对齐 | text-center |
| 两端对齐(浏览器不统一) | text-justify (慎用)|

### Bootstrap六种常用列表

- 普通列表和有序列表：只是加了margin-bottom: 10px;

- 去点列表list-unstyled：list-style-none; padding-left: 0;

- 定义列表：dl,dt,dd稍微有修改。

- 水平定义列表dl-horizontal：含有媒体查询。

- 水平内联列表list-inline：list-style-none; padding-left: 0; margin-left: -5px;

- 并且ul-li：display: inline-block; padding-right: 5px; padding-left: 5px;

### 三种代码书写和引入的风格

- code和kbd只是配色不同，pre用于多行代码输入，且计算空格。样式请看源码。

- 无论哪一种代码风格，碰到标签开始和结束符号都要使用硬编码“&lt”和“&gt”来代替。

- 添加.pre-scrollable类可以控制最大高度为340px，超出则出现垂直滚动条，宽度的控制使用稍后讲解的col-md-n。

### 表格

- 1个基础样式，4个附加样式，1个响应式表格够不够？表格行的背景色可以通过给tr添加六个相应颜色类名修改：
```
active(#f5f5f5)
success(#dff0d8)
info(#d9edf7)
warning(#fcf8e3)
danger(#f2dede)
```

- table加上.table-hover，同时tr加上字体颜色，这样也会有额外的伪类样式导致颜色悬浮。

|       表格类名          |      表格类型      |
|:--------------------:|:-----------------:|
|            .table            |      基础表格     |
|   .table-bordered   |  带边框的表格 |
|     .table-striped     |   斑马线表格    |
|      .table-hover      |  鼠标悬停高亮  |
|  .table-condensed |   紧凑型表格    |
|  .table-responsive |   响应式表格    |

- 基础表格默认设置了底边距20px，thead底部设置了2px的浅灰色实线，每个单元格顶部设置了1px的浅灰色实线。

- 带边框的表格只在基础表格的情况下加上了垂直1px的浅灰色边框线。

- 斑马线表格隔行浅灰色(#f9f9f9)背景，利用的是CSS3的:nth-child实现，IE8及以下无效。

- 鼠标悬停高亮表格原理是设置了tr:hover伪类。

- 紧凑型表格的原理是将单元格的内边距由8px调整到5px。

- 响应式表格据说以768px宽度为界是否出现滚动条，但据我是用来看所有类型的表格都是响应式的。

### 表单

-

### 按钮

- Bootstrap3相比v2版本在按钮的CSS3特效上减少了很多，但是兼容做得更好了很多。按钮类可以放在任何标签中，个人建议放在button和a标签中，简单表单提交可以考虑放在type=submit的input中。

- 基本按钮(.btn)，默认按钮(.btn-default)按钮背景均为#fff，字体为#333，边框颜色为#ccc。和表格同样的道理，使用默认按钮前要先使用基本按钮。

- 按钮的风格也可以定制，基本还是那几个颜色，分别变成了.btn-primary，.btn-success，.btn-info，.btn-warning，.btn-danger，.btn-link。使用定制按钮前也要先加入基本按钮哦。

- 按钮的大小也是可以修改的哦，下表是四种尺寸按钮的对比：

|       按钮类名          |      描述     |           属性和值            |
|:--------------------:|:-----------:|:------------------------:|
|          .btn-lg           |      变大      | padding: 10px 16px; font-size: 18px; <br-line-height: 1.33; border-radius: 6px; |
|             .btn             |      正常      | padding: 6px 12px; font-size: 14px; <br-line-height: 1.43; border-radius: 4px; |
|         .btn-sm          |      变小      | padding: 5px 10px; font-size: 12px; <br-line-height: 1.5; border-radius: 3px; |
|          .btn-xs           |      超小      | padding: 1px 5px; font-size: 12px; <br-line-height: 1.5; border-radius: 3px; |

- 先使用.btn声明这是个按钮，再用块状按钮.btn-block类可以让用户自定义一个按钮的尺寸和样式，这样按钮就会充满整个容器，并且不会有任何padding和margin。

- 按钮分为活动状态和禁用状态：活动状态有悬浮:hover，点击:active，焦点:focus，在不同按钮配色风格下它们的表现是不同的。

- 禁用按钮用两种方法，分别是添加类名或者添加元素属性disabled，禁用按钮会降低透明度，不同配色风格下的外观有所不同，多数场合使用可以禁止链接添加元素属性，鼠标经过会提示禁止。

### 按钮组

- 按钮组一般配合矢量图标用于定制化分页，或者用来开发类似于word编辑器插件的UI部分，你只需要在一个带.btn-group类名的容器中连续写上多个button按钮即可。

- 按钮的样式颜色类依然可以使用，按钮容器中加入带图标类的span标签就可以实现矢量图标按钮，类名.btn-group只是将这些按钮联合在一起了并且使用了伪类和头尾按钮CSS3的圆角。
如果你想制作编辑器插件那种样式

### 图像

- Bootstrap3中图片的样式主要有
响应式图片(.img-responsive)，圆角图片(.img-rounded)，原形图片(.img-circle)，缩略图片(.img-thumbnail)。

- 如果你想控制图片的大小，建议在img标签的父容器上规定尺寸，严禁直接通过CSS样式直接修改img图片的大小。圆角圆形使用的CSS3效果在IE8及以下是不起作用的。

- `缩略图`还有专门的组件类.thumbnail，其实就是给图片加了个框，一般配合网格系统和超链接标签使用，包括各种js图片弹出框组件也可以这样实现。

### 图标

- 制作好矢量图标后，配合CSS3的font-face为其命名就可以实现icon类的效果。Bootstrap3可以免费使用glyphicons.com这个商业公司提供的几百个矢量图标，当然你也可以下载引入更受欢迎的Font Awesome矢量图标。

- 使用glyphicon的图标前需要引入theme.css文件，然后添加类名glyphicon 和对应的前缀为glyphicon-这种类名即可。

### 网格系统/栅格布局

- 熟练使用栅格布局是入门Bootstrap的标志，当你需要使用它时，必须先定义一个容器，添加带padding且用于居中类名.container，布满宽度的为.container-fluid。然后定义数据行.row，在数据行容器的基础上去定义数据列.col，数据列容器根据终端的分辨率有.col-lg-，.col-md-，.col-sm-，.col-xs-，等开头的，结尾加上一个1-12的数字，你可以填写多个.col数据列，但是它们想加不允许超过12，否则会换行重新计算。

- 栅格布局针对的终端有四种，分别以分768px，992px，1220px的宽度作为分水岭，其对应的容器宽度和每列宽度的数字请自行百度，后者通过便宜计算出来，并不是准确的60px，80px。

- 栅格布局需要一个主要的容器，容器中的row和col都可以看作是一层容器，不同列之间可以有列偏移，列排序，列嵌套等等。

### 下拉菜单

- 使用下拉列表必须先引入对应版本的jquery.js和bootstrap.js，下拉菜单的类名叫做dropdowm掉下来，几乎都要配合按钮使用。将按钮和列表同时放入一个声明了.dropdown类的容器中。

- 你的button除了按钮样式类，还必须声明 data-toggle="dropdown" ，其内容必须和外层容器的类名一致，建议不要修改。

- ul必须声明.dropdown-menu类，该类样式有display:none，原理就是DOM操作给其添加或者移除display:block的.open类。如果你想让按钮出现指向箭头，请在button容器内添加span元素，并且加入.caret类。

- 下拉列表的分割线可以添加一个空的li并追加.divider类，但我不是很建议这种做法。

- 对每一组的下拉列表还可以给一个头部类别总称，也叫`菜单标题`：菜单标题中不需要超链接a标签，同时其声明类为.dropdown-header。

- 下拉菜单的对齐方式默认为左对齐，你可以通过给ul追加.dropdown-menu-right或者pull-right修改，两者完全是一样的，但是在这之前你必须给父容器一个宽度，建议使用botstrap自带的栅格布局。

- 下拉菜单项的状态默认开启了悬浮和焦点状态的，你也可通过增加.active和.disabled修改为活跃和禁用状态。禁用状态只有鼠标悬浮会出现禁止标志。

- 考虑SEO的话，这些地方都应该添加id和对应的role，初学不必理会，或者复制官方组件代码进行修改。

### 导航

- 使用.nav声明导航，还要追加具体导航的样式类，或者说主题类，导航声明一般都是放在ul标签中，并且li中添加超链接标签a。

- `标签形导航`：nav-tabs;

- `胶囊形导航`：nav-pills;

- `垂直列表导航`：nav-stacked;

- `自适应导航`：nav-justified;多数时候和tabs，pills配合使用。

- `二级导航`：将li当作父容器，给它dropdown类，它的子容器a和下拉箭头caret不变，子容器ul添加dropdown-menu类即可。

- `面包屑导航`：这就是无极限分类的前端UI部分了，面包屑导航使用.breadcrumbs组件类名。官网建议使用ol有序列表，为了表示当前位置，最后一个li应该添加.active状态类。它的实现方式用了伪类:before，IE低用户不支持。

### 导航条

- 基本导航条只是在ul导航的基础上添加了一个父容器，加了两个类名：navbar navbar-default，前者是声明组件，后者声明样式主题。其样式可以修改为反色主题：nav-inverse；

- 导航条可以添加稍显不同的标题(当然你也可以修改为LOGO图和矢量图标，但是请自行注意默认内外边距)，添加标题请在父容器中添加带.navbar-header类的div，并且div容器中添加带.navbar-brand类的a容器标签，a标签中书写标题内容。

- 二级菜单的书写和导航是一样的，在 li 中添加.dropdown类，然后是必备的a标签(a必须设置的：data-toggle="dropdown" class="dropdown-toggle")和span.caret，以及带dropdown-menu类的ul标签。

- li的激活和禁用状态依然可以自行设置。

- 导航栏中的表单搜索是比较常用的，你只需要定义一个form表单容器，包含div和button按钮即可，把input输入框放入div容器中。按钮样式随意定制哦，美化输入框input的办法是为它添加.form-control类，div容器必须添加.form-group类。至于form的class，你需要添加.navbar-form，根据需求你还可以添加navbar-left/right让它浮动定位。

- `导航条按钮`：navbar-btn；`导航条文本`：navbar-text；`导航条链接`：navbar-link；这三个不是很建议使用，貌似用多了样式的间距会被打乱。

- 如果你想让导航条固定在顶部或者底部，只需要添加.navbar-fixed-top或者.navbar-fixed-bottom。
实际上最常用的导航条是上面的综合一下再加上响应式，`响应式导航条`在宽度小的时候会隐藏起来，非常利于移动端使用。这里重要书写又有点麻烦，我直接上图吧：
![响应式导航条代码](http://upload-images.jianshu.io/upload_images/3995745-d1a91d98b71b79e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 另外分页导航也是一个重要且常用的组件，分页导航其实只是一个ul无序列表。组件类名为.pagination，分页导航包括带页码的和带翻页的两种，添加.active表示当前页码。

- 我们一般的分页都是使用div-a或者div-span这种结构，但是bootstrap3使用了ul-li-a这种结构哦。

- `页码分页导航`：pagination-lg/sm即可，默认大小可以省略。

- `翻页分页导航`：上一页下一页的类名分别为：.previous 和 .next。左右方向箭头硬编码分别为：« 和 »。

### 高亮标签和徽章

- 标签和徽章的用法和意义几乎是一样的。标签有六中颜色风格，声明为.label，六种类名分别为label-default/primary/success/info/warning/danger。

- 网上一些显示火啊热啊的就是这样写的，加了额外的定位。

- 徽章也叫勋章，主要用途还是提示未读信息这种ajax传输的小量验证和判断数据，在你想要添加的地方使用.badge类声明就会默认添加，常在ul导航栏中见到徽章，在特定颜色风格的li中，其徽章.badge样式也会有所改变。

- 按钮徽章和徽章浮动(.pull-right)也是经常见到的使用场景。

- 标签和徽章在没有数据内容时候都是隐藏的，这是用CSS的:empty伪类元素将之设置为display:none。

### 警示框

- 个人认为警示框非常实用，典型如laravel-china，ruby-china和简书的发表文章，评论和回复消息，这种页面小内容改变一般会使用ajax交互方式，js和后端语言联通后随时判断后端接口返回的json数组中status的值，如果返回值为0则让js在指定区域显示警示框和返回错误提示msg。

- 同样的，使用.alert声明警示框(为了利于SEO优化，建议声明组件类的同时添加role名)，需要其他颜色的警示框请追加使用alert-success，alert-info，alert-warning，alert-danger。

- `可关闭的警示框`通过给容器添加alert-dismissable类，并且在容器内添加这样一行按钮代码即可:
```
 <button class="close" type="button" data-dismiss="alert">×</button>
```

- `带超链接的警示框`只是在容器内部使用a标签而已，但是不同颜色类型的警示框，其超链接样式也有些美化和修改。为了突出警示框内容时，我们也常常在容器中使用strong标签。

### 进度条

- 进度条的声明类名为.progress，该声明必须放在具有一定宽度的父容器中，并且建议具有自己的背景颜色。子容器使用.progress-bar这个类名，同时设置子容器的width百分比值即可，但这只是并不常用的默认进度条样式(深蓝色)。
- `彩色进度条`只需要在子容器中添加代表颜色的几个进度条类名即可，如：progress-bar-success，progress-bar-info，progress-bar-warning，progress-bar-danger。

- `静态条纹进度条`就是在上面的基础上给父容器添加了progress-striped类。

- `动态条纹进度条`在静态的基础上给父容器添加了.active类。实现方式利用了CSS3的animation，@keyframes创建动画效果，再利用CSS3线性渐变制作。

- 实现简单的`多种颜色的进度条层叠`，你只需要在父容器内部放置多个子容器，并为它们设置progress-bar 和 progress-bar-color即可。多种颜色层叠也是可以使用条纹和动态条纹的，只需要给子容器添加progress-bar-striped和active类即可。

- `带Label的进度条`是最常用的，其实你只需要在子容器中书写正常的HTML内容即可实现，0%的进度条可能存在颜色不方便区分的问题。Bootstrap3考虑到语义化和SEO优化，建议添加使用role="progressbar" aria-valuenow="20" aria-valuemin="0" aria-valuemax="100"。

### 媒体对象

- 什么是媒体对象呢？移动APP上文章垂直布局在bootstrap3中就被称为媒体对象，一般是左边一张图，右边是内容的说明。

- 默认媒体对象在声明媒体对象容器(.media)后添加媒体对象的对象(.media-object)，也就是你常见的左侧图片。媒体对象的主体(.media-body)，就是右侧内容部分。主体中可以存在媒体对象的标题(.media-heading)。

- 除此之外，Bootstrap可以使用.pull-left和.pull-right控制媒体对象的浮动方式。通常情况你是这样操作的：
> 父容器添加.media类，内部分为带pull-left的a标签(内部有img图像)和带media-body的另一容器，.media-body容器中可以有一般为标题的.media-heading和尾部的footer。

### 媒体对象嵌套

- 媒体对象嵌套是评论系统必备的组件，一般是左侧用户头像等信息，右侧为用户评论的内容，这就是Bootstrap3中的媒体对象嵌套，只需将新的 .media容器放入.media-body中即可。

- 这个组件一般要配合无极限分类使用，但是评论系统使用无极限分类会导致数据结构层级太深，而且样式缩进对移动端用户不友好，建议后端使用无极限分类api，前端样式建议最多遍历到第三层。

- 媒体对象列表：对于前端样式不缩进，或者可以隐藏缩进只显示第一层评论的情况，Bootstrap3提供了可以给ul加上.media-list，给li加上.media的做法。一般情况下你的操作应该是这样的：给ul添加.media-list，多个li标签均添加.media类，li标签中包含左侧a容器(pull-left)和右侧div容器(media-body)，
左侧容器中包含一张img图片，右侧容器中可以包含heading，footer等，分别可以放在各种容器标签中。

### 列表组

- 基础的列表组就是给 ul 一个声明类 .list-group，再给所有的 li 一个 .list-group-item。
带徽章的列表组就在 li 中嵌套一个类名为 .badge的span标签，这样徽章就会出现在列表项的右侧，你也可以通过自定义样式文件增加 .badge 并增加color和background-color修改徽章的前景色和背景色。

- 带超链接的列表组就是 li 容器中加超链接 a 标签。

- 自定义列表组就是在 li 容器中其他标签上加入list-group-item-heading/text类，两者的区别是heading外边距距顶部0px,距底部5px; text外边距距底部0px，行高1.3倍。看起来就是text显得更加紧凑了。

- 列表组的状态可以设置为活动(.active)和禁用(.disabled)，分别给了li蓝色背景和灰色背景，并且禁用状态出现禁止标志。

- 多彩列表组只是修改了 li 的前景色和背景色。只要给 li 加入 list-group-item-success/info/warning/danger这些颜色类名就OK了。

### 面板

- 无论在PC还是移动端，面板配合栅格布局的使用率还是很高的，尤其是文章列表和行列商品展示，但是在v4版本有了新的替代品组件。 .spanel是面板声明类，具体包括基础面板(.panel-default)，带头尾的面板(-heading，-body，-footer)，面板中嵌套表格，面板中嵌套列表组(.list-group)，彩色风格的面板：
```
重点蓝-primary
信息蓝-info
成功绿-success
警告黄-warning
危险红-danger。
```
