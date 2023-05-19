---
layout: default
title: "Blogs"
permalink: /blogs/
author_profile: true
---

<link rel="stylesheet" href="/assets/css/responsive.css">
<link rel="stylesheet" href="/assets/css/index.css">

<div id="main" role="main">
{% include sidebar.html %}
<section class="container content">
    <div class="columns">
        <div class="column comment-position">
            <article class="article-content markdown-body">
                <section class="container posts-content">
                    {% assign sorted_tags = site.tags | sort %}
                    {% for category in sorted_tags %}
                    <h2>{{ category | first }}</h2>
                    <ol class="posts-list" id="{{ category[0] }}">
                        {% for post in category.last %}
                        <li class="posts-list-item">
                            <span class="posts-list-meta">{{ post.date | date:"%Y-%m-%d" }}</span> <a class="posts-list-name" href="{{ post.url }}">{{ post.title }}</a>
                        </li>
                        {% endfor %}
                    </ol>
                    {% endfor %}
                </section>
                <!-- /section.content -->
            </article>
        </div>
        <div class="column list-position">
            {% include sidebar-tags-nav.html %}
        </div>
    </div>
</section>
</div>