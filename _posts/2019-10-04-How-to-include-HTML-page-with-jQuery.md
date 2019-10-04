---
layout:     post
title:      "How to include HTML page with jQuery"
subtitle:   ""
date:       2019-10-04
author:     "LiuBiyongge"
header-img: "img/in-post/Web.png"
tags:

  - Java Web
---

# How to include HTML page with jQuery

[TOC]

## load() method

### 1. Create Embedding file

header.html

```html
<ul class='menu'>
 <li><a class="active" href="#home">Home</a></li>
 <li><a href="#about">About</a></li>
 <li><a href="#blog">Blog</a></li>
 <li><a href="#contact">Contact</a></li>
</ul>
```

header.css

```html
/* Menu */
.menu {
 list-style-type: none;
 margin: 0;
 padding: 0;
 overflow: hidden;
 background-color: darkturquoise;
}

.menu li {
 float: left;
}

.menu li a {
 display: block;
 color: white;
 text-align: center;
 padding: 14px 16px;
 text-decoration: none;
}

.menu li a:hover {
 background-color: lightskyblue;
}
```

2. load()

```
<html>
 <head>
  <title>How to include HTML page with jQuery</title>
  <script src='jquery.js' type='text/javascript'></script> 
  <script type='text/javascript'>
   $(document).ready(function(){
   	$("head").append($("<link rel='stylesheet' href='css/header.css' type='text/css' />"));
    $( "#header" ).load( "header.html" );
   });
  </script>
 </head> 
 <body>
  <div id='header'></div>
  <div class='content'>Content</div>
 </body>
</html>
```

