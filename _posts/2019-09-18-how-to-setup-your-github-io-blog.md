---
layout:     post
title:      "Build my blog"
subtitle:   ""
date:       2019-09-18
author:     "LiuBiyongge"
header-img: "img/in-post/build_blog.png"
tags:
  - 搭建博客
---

- 这篇文章参考https://keysaim.github.io/post/blog/2017-08-15-how-to-setup-your-github-io-blog/搭建
- 我的博客界面如下

![img](/img/in-post/blog_face.png)

# 编写发布博客

`Jekyll`对于博文，都是要求放在`_posts`目录下面，同时对博文的文件名有[严格的规定](https://jekyllrb.com/docs/posts/#creating-post-files)，必须保持格式`YEAR-MONTH-DAY-title.MARKUP`，通常情况下，咱们采用推荐的`Markdown`撰写博文，基于该格式，本博文的文件名为`2019-09-18-how-to-setup-your-github-io-blog`。

写好博文之后，就可以通过`git`提交博文了：

```shell
$ git add _posts/2019-09-18-how-to-setup-your-github-io-blog
$ git commit -m "Add how to setup your github.io blog"
$ git push mine master
```

