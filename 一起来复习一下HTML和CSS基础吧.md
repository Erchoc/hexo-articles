---
title: 一起来复习一下HTML和CSS基础吧
date: 2017-03-16 12:13:05
tags: 基础学习
---

> 这篇文章是我根据学校图书馆一本讲HTML+CSS的基础书籍，花费半天时间看完并总结的，主要是针对我个人理解，写的可能有点乱让别看的有点郁闷了。这里的基础知识涉及到的也不多，都是w3c文档写的部分，建议到中国区w3cschool查看。

<!-- more -->

### HTML部分

- meta可以用于跳转网页

- 能用css实现的，就不要用图片实现！

- mete base属性已经几乎不用了

- 粗体尽量用语义化strong,`粗体最好的选择是用CSS font-weight`

- 斜体i,em,cite，尽量用em,`斜体最好的选择是CSS font-style`

- 指数上标用sup,下标sub

- 删除线s，下划线u,`CSS的text-decoration`

- 版权声明small

- 特殊符号表: 空格 `CSS缩进text-indent`

- inline元素里面放block元素？

- 有序列表，无序列表，定义列表

- type=1,a,A,i,I `CSS的list-style-type`

- type=disc,circle,square

- 表格标题caption,

- 表头th，行头tr,单元格td对应语义化: thead,tbody,tfoot

- 合并行rowspan, 合并列colspan

- 图片src,alt,title给搜索引擎和用户看

- 任何名字不要用中文

- 位图(点阵图)和矢量图(向量图)8/16/24/32位图

- 超链接的target:_self, _blank, _top, _parent(HTML框架)

- 内部链接、外部链接和锚点链接

- 常用表单元素:

  - input
  - textarea
  - select,option

- form标签属性:

  - name
  - action
  - method
  - enctype
  - target

- 表单对象的属性:

  - value
  - size
  - maxlength

- 复选框checkbox必须配合label和其for属性使用

- 表单按钮button, submit, reset

- 图片域: image属性

- 隐藏域: hidden属性

- 文件域: file属性，要声明编码方式enctype="multi/form-data"

- 多行文本框textarea: rows clos

- 下拉列表select+option属性:

  - multiple(Ctrl+鼠标左键选择多个)
  - size(显示的行数，其他出现滚动条)

- 在线音频视频用embed src

- frameset框架集标签被HTML5舍弃，用浮动框架iframe和scrolling属性: auto(默认左对齐),yes,no(滚动条)

### CSS部分

- 三种引入样式的办法: 外部样式表，内部样式表，内联样式表

- 注意: link在加载CSS后加载HTML，@import却先加载HTML再加载CSS

- id选择器也可以写成name，但是id是HTML的标准，name是XHTML的标准，尽量不用name。

- 子元素选择器，相邻选择器，群组选择器(#a,#b)

- 关于字体(类型，大小，粗细，斜体，颜色)

- 字体单位(关键字): xx-small, x-small, small, medium, large, x-large, xx-large

- 字体粗细(100-900): normal, lighter, bold, nolder

- 字体斜体(font-style): normal, italic, oblique(没有倾斜属性的特殊字体)

- 关于文本：用text-decoration取代s和u标签(空，下划线，删除线，顶划线)

- 用text-transform转换大小写(none, uppercase, lowercase, capitalize)

- font-variant小型大写字母(normal, small-caps)

- text-indent段落首行缩进

- p段落字体14px，则text-indent: 28px

- text-align文本和img水平对齐(left,center,right)

- line-height行高

- letter-spacing字距

- word-spacing词距

- 边框样式（border-width, border-color, border-style）
none, hidden, solid, dashed, dotted, double

- 3D: inset内, outset外, ridge脊, groove槽

- 简洁写法:border: 1px red solid;

- 局部边框样式:border-bottom

- 背景样式

- web2.0都在CSS中使用background

- background-color:背景颜色

- image:url()背景图像

- repeat:是否横纵平铺(no-repeat, repeat, repeat-x, repeat-y)

- position:图像显示位置(用法margin)top button left right

- attachment:是否随内容滚动(响应式)(默认scroll，可选fixed)

- 超链接伪类(必须按顺序定义)

  - a:link,未访问时
  - a:visited,访问后
  - a:hover,鼠标经过
  - a:actived，单击激活时
  - :hover伪类可以定义于每个元素！

- 浏览器鼠标样式cursor: pointer,default,wait,help等等。

- 自定义鼠标样式cursor:url(" "),属性;

- 图片水平对齐用text-align

- 垂直对齐用vertical-align(top,middle,baseline,bottom)

- 文字环绕效果float(图文混排)

- 列表样式:统一使用list-style-type

- 无序ul列表:(decimal,lower-roman,upper-romam,lower-alpha,upper-alpha)

- 有序ol列表:(disc,circle,square,none)

- 自定义列表项符号:list-style-image: url();

- 表格样式,边框合并和边框间距border-collapse(默认sqparate,collapse)

- border-spacing:(一或两个像素参数)

- 标题位置caption-side(top,bottom)

- CSS盒子模型(块元素和行内元素)

- content-padding-margin-border四大属性

- content区三属性:width,height,overflow

- 宽高属于内容区，不包括"补白"，溢出属性用于处理超出内容区的范围

- 负margin重叠技术,行内变块级display:block;

- 浮动布局和定位布局

- CSS: 正常文档流和脱离文档流relative，absolute，fixed，默认是静态定位static

- 相对定位元素始终会获得相应的空间

- 绝对定位和固定定位会完全脱离文档流
