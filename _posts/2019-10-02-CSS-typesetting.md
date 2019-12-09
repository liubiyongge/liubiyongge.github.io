---
layout:     post
title:      "CSS 排版"
subtitle:   ""
date:       2019-10-03
author:     "LiuBiyongge"
header-img: "img/in-post/bootstrap.png"
tags:

  - Java Web
---

# 前端排版问题

[TOC]



## 浏览器放缩问题

- 最外面再套一层div，然后给这个div赋一个固定的长宽

## 文本的对齐

- text-align是怎样个对齐法?

文字在Content框中对齐

## BOX模型

```
一定要border的样式，宽度，颜色都要设置才可以的！！ 
```

![CSS box-model](https://www.runoob.com/images/box-model.gif)

![img](https://www.runoob.com/wp-content/uploads/2013/08/VlwVi.png)

## Display

### 块和内联元素

块元素是一个元素，占用了全部宽度，在前后都是换行符。

块元素的例子：

- `<h1>`
- `<p>`
- `<div>`

内联元素只需要必要的宽度，不强制换行。

内联元素的例子：

- `<span>`
- `<a>`

### 块元素和内联元素互换

`li {display:inline;}`

`span {display:block;}`

### 块级元素与内联元素特点

**块级元素(block)特性：**

- 总是独占一行，表现为另起一行开始，而且其后的元素也必须另起一行显示;
- 宽度(width)、高度(height)、内边距(padding)和外边距(margin)都可控制;

**内联元素(inline)特性：**

- 和相邻的内联元素在同一行;
- 宽度(width)、高度(height)、内边距的top/bottom(padding-top/padding-bottom)和外边距的top/bottom(margin-top/margin-bottom)都不可改变，就是里面文字或图片的大小;

**块级元素主要有：**

-  address , blockquote , center , dir , div , dl , fieldset , form , h1 , h2 , h3 , h4 , h5 , h6 , hr , isindex , menu , noframes , noscript , ol , p , pre , table , ul , li

**内联元素主要有：**

- a , abbr , acronym , b , bdo , big , br , cite , code , dfn , em , font , i , img , input , kbd , label , q , s , samp , select , small , span , strike , strong , sub , sup ,textarea , tt , u , var

**可变元素(根据上下文关系确定该元素是块元素还是内联元素)：**

- applet ,button ,del ,iframe , ins ,map ,object , script

**CSS中块级、内联元素的应用：**

利用CSS我们可以摆脱上面表格里HTML标签归类的限制，自由地在不同标签/元素上应用我们需要的属性。

主要用的CSS样式有以下三个：

- display:block  -- 显示为块级元素
- display:inline  -- 显示为内联元素
- display:inline-block -- 显示为内联块元素，表现为同行显示并可修改宽高内外边距等属性

我们常将<ul>元素加上display:inline-block样式，原本垂直的列表就可以水平显示了。

> 块级元素对齐通过margin实现，内联元素对齐通过text-align实现，text-align 属性规定元素中的文本的水平对齐方式。

## Position

### static 定位

HTML 元素的默认值，即没有定位，遵循正常的文档流对象。

静态定位的元素不会受到 top, bottom, left, right影响。

```
div.static {
    position: static;
    border: 3px solid #73AD21;
}
```

### fixed 定位

元素的位置相对于浏览器窗口是固定位置。

即使窗口是滚动的它也不会移动：

### relative 定位

相对定位元素的定位是相对其正常位置。

### absolute 定位

绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于`<html>`:

### sticky 定位

sticky 英文字面意思是粘，粘贴，所以可以把它称之为粘性定位。

**position: sticky;** 基于用户的滚动位置来定位。

粘性定位的元素是依赖于用户的滚动，在 **position:relative** 与 **position:fixed** 定位之间切换。

## Overflow

CSS overflow 属性用于控制内容溢出元素框时显示的方式。

overflow属性有以下值：

| 值      | 描述                                                     |
| :------ | :------------------------------------------------------- |
| visible | 默认值。内容不会被修剪，会呈现在元素框之外。             |
| hidden  | 内容会被修剪，并且其余内容是不可见的。                   |
| scroll  | 内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。 |
| auto    | 如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。 |
| inherit | 规定应该从父元素继承 overflow 属性的值。                 |

## Float

CSS 的 Float（浮动），会使元素向左或向右移动，其周围的元素也会重新排列。

Float（浮动），往往是用于图像，但它在布局时一样非常有用。

元素的水平方向浮动，意味着元素只能左右移动而不能上下移动。

一个浮动元素会尽量向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。

浮动元素之后的元素将围绕它。

浮动元素之前的元素将不会受到影响。

## 水平 & 垂直对齐

### 元素居中对齐

要水平居中对齐一个元素(如 `<div>`), 可以使用 **margin: auto;**。

设置到元素的宽度将防止它溢出到容器的边缘。

元素通过指定宽度，并将两边的空外边距平均分配：

**注意:** 如果没有设置 **width** 属性(或者设置 100%)，居中对齐将不起作用。

- 相对于谁居中?

相对于box居中

- width百分比是什么意思

content的width占整个box(包括margin)的百分比

### 文本居中对齐

如果仅仅是为了文本在元素内居中对齐，可以使用 **text-align: center;**

- 相对于谁居中?

文本相对于content居中

### 左右对齐

- 我们可以使用 **position: absolute;** 属性来对齐元素:
- 左右对齐 - 使用 float 方式

我们可以在父元素上添加 overflow: auto; 来解决子元素溢出的问题:

### 垂直居中对齐 - 使用 padding

CSS 中有很多方式可以实现垂直居中对齐。 一个简单的方式就是头部顶部使用 **padding**: