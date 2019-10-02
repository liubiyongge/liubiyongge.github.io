---
layout:     post
title:      "JQuery Note"
subtitle:   ""
date:       2019-10-02
author:     "LiuBiyongge"
header-img: "img/in-post/JQuery.jpg"
tags:

  - Java Web
---
# JQuery note

[TOC]

- HTML 元素选取
- HTML 元素操作
- CSS操作
- HTML事件函数
- JavaScript特效和动画
- HTML DOM遍历和修改
- AJAX
- Utilities

## JQuery 语法

`$(selector).action()`

```
$(document).ready(function(){ 
// 开始写 jQuery 代码...   
});

or 

$(function(){
 
   // 开始写 jQuery 代码...
 
});
```

这是为了防止文档在完全加载（就绪）之前运行 jQuery 代码，即在 DOM 加载完成后才可以对 DOM 进行操作。

### selector

`S("p")` `<p>`

`#id` 

`.class`

| 语法                     | 描述                                                    | 实例                                                         |
| :----------------------- | :------------------------------------------------------ | :----------------------------------------------------------- |
| $("*")                   | 选取所有元素                                            | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_all2) |
| $(this)                  | 选取当前 HTML 元素                                      | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_this) |
| $("p.intro")             | 选取 class 为 intro 的 <p> 元素                         | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_pclass) |
| $("p:first")             | 选取第一个 <p> 元素                                     | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_pfirst) |
| $("ul li:first")         | 选取第一个 <ul> 元素的第一个 <li> 元素                  | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_ullifirst) |
| $("ul li:first-child")   | 选取每个 <ul> 元素的第一个 <li> 元素                    | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_ullifirstchild) |
| $("[href]")              | 选取带有 href 属性的元素                                | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_hrefattr) |
| $("a[target='_blank']")  | 选取所有 target 属性值等于 "_blank" 的 <a> 元素         | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_hrefattrblank) |
| $("a[target!='_blank']") | 选取所有 target 属性值不等于 "_blank" 的 <a> 元素       | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_hrefattrnotblank) |
| $(":button")             | 选取所有 type="button" 的 <input> 元素 和 <button> 元素 | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_button2) |
| $("tr:even")             | 选取偶数位置的 <tr> 元素                                | [在线实例](https://www.runoob.com/try/try.php?filename=tryjquery_sel_even) |
| $("tr:odd")              | 选取奇数位置的 <tr> 元素                                |                                                              |

### JQuery 事件

- 在元素上移动鼠标
- 选取单选按钮
- 点击元素

| 鼠标事件                                                     | 键盘事件                                                     | 表单事件                                                  | 文档/窗口事件                                             |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :-------------------------------------------------------- | :-------------------------------------------------------- |
| [click](https://www.runoob.com/jquery/event-click.html)      | [keypress](https://www.runoob.com/jquery/event-keypress.html) | [submit](https://www.runoob.com/jquery/event-submit.html) | [load](https://www.runoob.com/jquery/event-load.html)     |
| [dblclick](https://www.runoob.com/jquery/event-dblclick.html) | [keydown](https://www.runoob.com/jquery/event-keydown.html)  | [change](https://www.runoob.com/jquery/event-change.html) | [resize](https://www.runoob.com/jquery/event-resize.html) |
| [mouseenter](https://www.runoob.com/jquery/event-mouseenter.html) | [keyup](https://www.runoob.com/jquery/event-keyup.html)      | [focus](https://www.runoob.com/jquery/event-focus.html)   | [scroll](https://www.runoob.com/jquery/event-scroll.html) |
| [mouseleave](https://www.runoob.com/jquery/event-mouseleave.html) |                                                              | [blur](https://www.runoob.com/jquery/event-blur.html)     | [unload](https://www.runoob.com/jquery/event-unload.html) |
| [hover](https://www.runoob.com/jquery/event-hover.html)(定义函数) |                                                              |                                                           |                                                           |
| mousedown                                                    |                                                              |                                                           |                                                           |
| mouseup                                                      |                                                              |                                                           |                                                           |

### JQuery效果

`  $(selector).hide(speed,callback);`

`$(selector).show(speed,callback);  `

`$(selector).toggle(speed,callback);`

`$(selector).fadeIn(speed,callback);`

`$(selector).fadeOut(speed,callback);`

`$(selector).fadeToggle(speed,callback);`

`$(selector).fadeTo(speed,opacity,callback);`

`$(selector).slideDown(speed,callback);`

`$(selector).slideUp(speed,callback);`

`$(selector).slideToggle(speed,callback);`

`$(selector).animate({params},speed,callback);`

`$(selector).stop(stopAll,goToEnd);`

jQuery 方法链接

 `$("#p1").css("color","red").slideUp(2000).slideDown(2000);`

## JQuery HTML

`设置`

- text() - 设置或返回所选元素的文本内容
- html() - 设置或返回所选元素的内容（包括 HTML 标记）
- val() - 设置或返回表单字段的值
- attr() - 获取属性

`添加元素`

- append() - 在被选元素的结尾插入内容（仍然该元素的内部）
- prepend() - 在被选元素的开头插入内容（仍然该元素的内部）
- after() - 在被选元素之后插入内容
- before() - 在被选元素之前插入内容

`删除元素`

- remove() - 删除被选元素（及其子元素）
- empty() - 从被选元素中删除子元素

`css类`

- addClass() - 向被选元素添加一个或多个类
- removeClass() - 从被选元素删除一个或多个类
- toggleClass() - 对被选元素进行添加/删除类的切换操作
- css("*propertyname*","*value*"); - 设置或返回样式属性
- css({"*propertyname*":"*value*","*propertyname*":"*value*",...});

`尺寸方法`

- width()
- height()
- innerWidth()
- innerHeight()
- outerWidth()
- outerHeight()

![jQuery Dimensions](https://www.runoob.com/images/img_jquerydim.gif)

## jQuery 遍历

`祖先`

- parent()
- parents()
- parentsUntil()

`后代`

- children()
- find()

`同胞`

- siblings()
- next()
- nextAll()
- nextUntil()
- prev()
- prevAll()
- prevUntil()

`过滤`

三个最基本的过滤方法是：first(), last() 和 eq()，它们允许您基于其在一组元素中的位置来选择一个特定的元素。

其他过滤方法，比如 filter() 和 not() 允许您选取匹配或不匹配某项指定标准的元素。

## AJAX

在不重载整个网页的情况下，AJAX 通过后台加载数据，并在网页上进行显示。

`load`

$(selector).load(URL,data,callback);

必需的 *URL* 参数规定您希望加载的 URL。

可选的 *data* 参数规定与请求一同发送的查询字符串键/值对集合。

可选的 *callback* 参数是 load() 方法完成后所执行的函数名称。

可选的 callback 参数规定当 load() 方法完成后所要允许的回调函数。回调函数可以设置不同的参数：

- *responseTxt* - 包含调用成功时的结果内容
- *statusTXT* - 包含调用的状态
- *xhr* - 包含 XMLHttpRequest 对象

`get()`

$.get(*URL*,*callback*);

`post()`