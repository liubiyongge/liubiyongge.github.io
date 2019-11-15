---
layout: post
title: "Maven Note"
subtitle: ""
date: 2019-11-13
author: "LiuBiyongge"
header-img: "img/in-post/all.jpg"
tags:
 - Java Web
---

# Maven Note[^1]

[TOC]

- **plugin** is a collection of *goals* with a general common purpose 

### Filtering resource files[^2]

 Sometimes a resource file will need to contain a value that can only be supplied at build time.

>  Filtering作用是用环境变量、pom文件里定义的属性和指定配置文件里的属性替换属性(`*.properties`)文件里的占位符 ${<property name>} 
>
> `<properties></properties>`设置属性
>
> ` <filters><filter></filter></filters>`设置哪些文件需要属性替换
>
> `<filtering>true</filtering>`设置整个文件夹内文件都需要属性替换

___

在`src/main/resources`目录有个配置文件`jdbc.properties`，内容如下：

```
jdbc.url=${pom.jdbc.url}
jdbc.username=${pom.jdbc.username}
jdbc.passworkd=${pom.jdbc.password}
```

配置 resource 插件，启用filtering功能并添加属性到pom:

```
<project>
    ...
    <!-- 用pom里定义的属性做替换 -->    
    <properties>
        <pom.jdbc.url>jdbc:mysql://127.0.0.1:3306/dev</pom.jdbc.url>
        <pom.jdbc.username>root</pom.jdbc.username>
        <pom.jdbc.password>123456</pom.jdbc.password>
    </properties>
    <build>
      ...
        <!-- 可以把属性写到文件里,用属性文件里定义的属性做替换 -->
        <filters>
            <filter>src/main/filters.properties</filter>
        </filters>
        <resources>
          <resource>
            <directory>src/main/resources</directory>
            <filtering>true</filtering>
          </resource>
        </resources>
        ...
    </build>
    ...
</project>
```

编译包后`target`目录下的`jdbc.properties`:

```CQL
jdbc.url=jdbc:mysql://127.0.0.1:3306/dev
jdbc.username=root
jdbc.passworkd=123456
```

[^1]: https://maven.apache.org/guides/getting-started/index.html 
[^2]: https://segmentfault.com/a/1190000003908040

