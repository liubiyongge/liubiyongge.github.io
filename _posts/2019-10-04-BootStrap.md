---
layout:     post
title:      "BootStrap Study"
subtitle:   ""
date:       2019-10-04
author:     "LiuBiyongge"
header-img: "img/in-post/Web.png"
tags:

  - Java Web
---

# BootStrap

[TOC]

## BootStrap Grid System

`BootStrap提供一套响应式、移动设备优先的流式网格系统，随着屏幕或视口尺寸的增加，系统会自动分为最多12列。`

**流式布局：**
流式布局在CSS2时代就有，主要是靠百分比进行排版，可以在不同分辨率下显示相同的版式。

流式布局：网页中主要的划分区域的尺寸使用百分数（搭配min-*、max-*属性使用），例如，设置网页主体的宽度为80%，min-width为960px。图片也作类似处理（width:100%, max-width一般设定为图片本身的尺寸，防止被拉伸而失真）。

这种布局方式在Web前端开发的早期历史上，用来应对不同尺寸的PC屏幕（那是屏幕尺寸的差异不会太大），在当今的移动端开发也是常用布局方式，但缺点明显：宽度使用百分比定义，但是高度和文字大小等大都是用px来固定，所以在大屏幕的手机下显示效果会变成有些页面元素宽度被拉的很长，但是高度、文字大小还是和原来一样（即，这些东西无法变得“流式”），显示非常不协调。


**移动设备优先策略**

- 内容
  - 决定什么是最重要的。
- 布局
  - 优先设计更小的宽度。
  - 基础的 CSS 是移动设备优先，媒体查询是针对于平板电脑、台式电脑。
- 渐进增强
  - 随着屏幕大小的增加而添加元素。



### 工作原理

- 行必须放置在 **.container** class 内，以便获得适当的对齐（alignment）和内边距（padding）。

```
.container {
   padding-right: 15px;
   padding-left: 15px;
   margin-right: auto;
   margin-left: auto;
}
```

- 使用行来创建列的水平组。
- 内容应该放置在列内，且唯有列可以是行的直接子元素。
- 预定义的网格类，比如 **.row** 和 **.col-xs-4**，可用于快速创建网格布局。LESS 混合类可用于更多语义布局。
- 列通过内边距（padding）来创建列内容之间的间隙。该内边距是通过 **.rows** 上的外边距（margin）取负，表示第一列和最后一列的行偏移。
- 网格系统是通过指定您想要横跨的十二个可用的列来创建的。例如，要创建三个相等的列，则使用三个 **.col-xs-4**。

#### 媒体查询

媒体查询是非常别致的"有条件的 CSS 规则"。它只适用于一些基于某些规定条件的 CSS。如果满足那些条件，则应用相应的样式。

Bootstrap 中的媒体查询允许您基于视口大小移动、显示并隐藏内容。下面的媒体查询在 LESS 文件中使用，用来创建 Bootstrap 网格系统中的关键的分界点阈值。

```
/* 超小设备（手机，小于 768px） */
/* Bootstrap 中默认情况下没有媒体查询 */

/* 小型设备（平板电脑，768px 起） */
@media (min-width: @screen-sm-min) { ... }

/* 中型设备（台式电脑，992px 起） */
@media (min-width: @screen-md-min) { ... }

/* 大型设备（大台式电脑，1200px 起） */
@media (min-width: @screen-lg-min) { ... }
```

#### 网格选项

下表总结了 Bootstrap 网格系统如何跨多个设备工作：

|              | 超小设备手机（<768px）         | 小型设备平板电脑（≥768px）     | 中型设备台式电脑（≥992px）     | 大型设备台式电脑（≥1200px）    |
| :----------- | :----------------------------- | :----------------------------- | :----------------------------- | :----------------------------- |
| 网格行为     | 一直是水平的                   | 以折叠开始，断点以上是水平的   | 以折叠开始，断点以上是水平的   | 以折叠开始，断点以上是水平的   |
| 最大容器宽度 | None (auto)                    | 750px                          | 970px                          | 1170px                         |
| Class 前缀   | **.col-xs-**                   | **.col-sm-**                   | **.col-md-**                   | **.col-lg-**                   |
| 列数量和     | 12                             | 12                             | 12                             | 12                             |
| 最大列宽     | Auto                           | 60px                           | 78px                           | 95px                           |
| 间隙宽度     | 30px （一个列的每边分别 15px） | 30px （一个列的每边分别 15px） | 30px （一个列的每边分别 15px） | 30px （一个列的每边分别 15px） |
| 可嵌套       | Yes                            | Yes                            | Yes                            | Yes                            |
| 偏移量       | Yes                            | Yes                            | Yes                            | Yes                            |
| 列排序       | Yes                            | Yes                            | Yes                            | Yes                            |

#### 响应式的列重置

#### 偏移列

偏移是一个用于更专业的布局的有用功能。它们可用来给列腾出更多的空间。例如，**.col-xs-\*** 类不支持偏移，但是它们可以简单地通过使用一个空的单元格来实现该效果。

为了在大屏幕显示器上使用偏移，请使用 **.col-md-offset-\*** 类。这些类会把一个列的左外边距（margin）增加 ***** 列，其中 ***** 范围是从 **1** 到 **11**。

在下面的实例中，我们有 `<div class="col-md-6">..</div>`，我们将使用 **.col-md-offset-3** class 来居中这个 div。

#### 嵌套列

为了在内容中嵌套默认的网格，请添加一个新的 **.row**，并在一个已有的 **.col-md-\*** 列内添加一组 **.col-md-\*** 列。被嵌套的行应包含一组列，这组列个数不能超过12（其实，没有要求你必须占满12列）。

在下面的实例中，布局有两个列，第二列被分为两行四个盒子。

#### 列排序

Bootstrap 网格系统另一个完美的特性，就是您可以很容易地以一种顺序编写列，然后以另一种顺序显示列。

您可以很轻易地改变带有 **.col-md-push-\*** 和 **.col-md-pull-\*** 类的内置网格列的顺序，其中 ***** 范围是从 **1** 到 **11**。

在下面的实例中，我们有两列布局，左列很窄，作为侧边栏。我们将使用 **.col-md-push-\*** 和 **.col-md-pull-\*** 类来互换这两列的顺序。

### Bootstrap 排版

- 标题
- 内联子标题
- 引导主体副本
- 强调
- 缩写
- 地址
- 列表
- 代码
- 表格
- 表单
- 按钮
- 图片

### Bootstrap 响应式实用工具

**响应式实用工具目前只适用于块和表切换**

| 超小屏幕 手机 (<768px) | 小屏幕 平板 (≥768px) | 中等屏幕 桌面 (≥992px) | 大屏幕 桌面 (≥1200px) |      |
| :--------------------- | :------------------- | :--------------------- | :-------------------- | ---- |
| .visible-xs-*          | 可见                 | 隐藏                   | 隐藏                  | 隐藏 |
| .visible-sm-*          | 隐藏                 | 可见                   | 隐藏                  | 隐藏 |
| .visible-md-*          | 隐藏                 | 隐藏                   | 可见                  | 隐藏 |
| .visible-lg-*          | 隐藏                 | 隐藏                   | 隐藏                  | 可见 |
| .hidden-xs             | 隐藏                 | 可见                   | 可见                  | 可见 |
| .hidden-sm             | 可见                 | 隐藏                   | 可见                  | 可见 |
| .hidden-md             | 可见                 | 可见                   | 隐藏                  | 可见 |
| .hidden-lg             | 可见                 | 可见                   | 可见                  | 隐藏 |

## BootStrap 布局组件

- 字体图标
- 按钮组
- 按钮下拉菜单
- Bootstrap 输入框组
- Bootstrap 分页
- Bootstrap 标签
- Bootstrap 徽章（Badges）
- Bootstrap 超大屏幕（Jumbotron）
- 页面标签
- 缩略图
- Bootstrap 警告
- Bootstrap 进度条
- Bootstrap 多媒体对象
- Bootstrap 列表组
- Bootstrap 面板
- Bootstrap Well
- 

### 下拉菜单

```
	<link rel="stylesheet" href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css">
	<script src="https://cdn.staticfile.org/jquery/2.1.1/jquery.min.js"></script>
	<script src="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/js/bootstrap.min.js"></script>
```



```
<div class="dropdown">
    <button type="button" class="btn dropdown-toggle" id="dropdownMenu1" data-toggle="dropdown">主题
        <span class="caret"></span>
    </button>
    <ul class="dropdown-menu" role="menu" aria-labelledby="dropdownMenu1">
        <li role="presentation">
            <a role="menuitem" tabindex="-1" href="#">Java</a>
        </li>
        <li role="presentation">
            <a role="menuitem" tabindex="-1" href="#">数据挖掘</a>
        </li>
        <li role="presentation">
            <a role="menuitem" tabindex="-1" href="#">数据通信/网络</a>
        </li>
        <li role="presentation" class="divider"></li>
        <li role="presentation">
            <a role="menuitem" tabindex="-1" href="#">分离的链接</a>
        </li>
    </ul>
</div>
```

- 对齐

通过向 **.dropdown-menu** 添加 class **.pull-right** 来向右对齐下拉菜单。下面的实例演示了这点：

- 标题

您可以使用 class **dropdown-header** 向下拉菜单的标签区域添加标题。下面的实例演示了这点

### Bootstrap 导航元素

### Bootstrap 导航栏

#### 默认的导航栏

创建一个默认的导航栏的步骤如下：

- 向 `<nav>` 标签添加 class **.navbar、.navbar-default**。
- 向上面的元素添加 **role="navigation"**，有助于增加可访问性。
- 向` <div>` 元素添加一个标题 class **.navbar-header**，内部包含了带有 class **navbar-brand** 的 `<a>` 元素。这会让文本看起来更大一号。
- 为了向导航栏添加链接，只需要简单地添加带有 class **.nav、.navbar-nav** 的无序列表即可。

```
<nav class="navbar navbar-default" role="navigation">
    <div class="container-fluid">
    <div class="navbar-header">
        <a class="navbar-brand" href="#">菜鸟教程</a>
    </div>
    <div>
        <ul class="nav navbar-nav">
            <li class="active"><a href="#">iOS</a></li>
            <li><a href="#">SVN</a></li>
            <li class="dropdown">
                <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                    Java
                    <b class="caret"></b>
                </a>
                <ul class="dropdown-menu">
                    <li><a href="#">jmeter</a></li>
                    <li><a href="#">EJB</a></li>
                    <li><a href="#">Jasper Report</a></li>
                    <li class="divider"></li>
                    <li><a href="#">分离的链接</a></li>
                    <li class="divider"></li>
                    <li><a href="#">另一个分离的链接</a></li>
                </ul>
            </li>
        </ul>
    </div>
    </div>
</nav>
```

#### 响应式的导航栏

为了给导航栏添加响应式特性，您要折叠的内容必须包裹在带有 class **.collapse、.navbar-collapse** 的 <div> 中。折叠起来的导航栏实际上是一个带有 class **.navbar-toggle** 及两个 data- 元素的按钮。第一个是 **data-toggle**，用于告诉 JavaScript 需要对按钮做什么，第二个是 **data-target**，指示要切换到哪一个元素。三个带有 class **.icon-bar** 的 <span> 创建所谓的汉堡按钮。这些会切换为 **.nav-collapse** <div> 中的元素。为了实现以上这些功能，您必须包含 [Bootstrap 折叠（Collapse）插件](https://www.runoob.com/bootstrap/bootstrap-collapse-plugin.html)。

```
<nav class="navbar navbar-default" role="navigation">
    <div class="container-fluid"> 
    <div class="navbar-header">
        <button type="button" class="navbar-toggle" data-toggle="collapse"
                data-target="#example-navbar-collapse">
            <span class="sr-only">切换导航</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
        </button>
        <a class="navbar-brand" href="#">菜鸟教程</a>
    </div>
    <div class="collapse navbar-collapse" id="example-navbar-collapse">
        <ul class="nav navbar-nav">
            <li class="active"><a href="#">iOS</a></li>
            <li><a href="#">SVN</a></li>
            <li class="dropdown">
                <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                    Java <b class="caret"></b>
                </a>
                <ul class="dropdown-menu">
                    <li><a href="#">jmeter</a></li>
                    <li><a href="#">EJB</a></li>
                    <li><a href="#">Jasper Report</a></li>
                    <li class="divider"></li>
                    <li><a href="#">分离的链接</a></li>
                    <li class="divider"></li>
                    <li><a href="#">另一个分离的链接</a></li>
                </ul>
            </li>
        </ul>
    </div>
    </div>
</nav>

```

#### 导航栏中的表单

```
<nav class="navbar navbar-default" role="navigation">
    <div class="container-fluid"> 
    <div class="navbar-header">
        <a class="navbar-brand" href="#">菜鸟教程</a>
    </div>
    <form class="navbar-form navbar-left" role="search">
        <div class="form-group">
            <input type="text" class="form-control" placeholder="Search">
        </div>
        <button type="submit" class="btn btn-default">提交</button>
    </form>
    </div>
</nav>
```

#### 导航栏中的按钮

#### 导航栏中的文本

#### 组件对齐方式

#### 固定到顶部

#### 反色的导航栏

### 面包屑导航

