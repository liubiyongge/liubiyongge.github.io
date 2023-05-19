## Layout Templates For All Page
```
_layouts/default.html
    _includes/head.html
    _includes/head/custom.html

    _includes/masthead.html

    {{ content }}

    _includes/footer/custom.html
    _includes/footer.html

```

## Navigation
信息配置 _data/navigation.yml
页码渲染 _includes/masthead.html

## Left SideBar
信息配置 _config.yml # Site Author
页码渲染 _includes/sidebar.html


## HomePage
信息配置 about.md

## Foot
信息配置 _config.yml
页码渲染 footer.html

