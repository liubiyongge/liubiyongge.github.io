---
layout:     post
title:      "spring boot documentatoin Read note"
subtitle:   ""
date:       2019-11-15
author:     "LiuBiyongge"
header-img: "img/in-post/Web.png"
tags:

  - Java Web
---



# spring boot documentation Read note

[TOC]

## Spring Boot Features

### SpringApplication

#### Fluent Builder API

1. `context`就是“容器”，放的就是应用程序的所有资源，要用时候就访问它，所以`context`里面的东西，在同一个应用程序里面是全局的；web上下文可以看成web应用的运行环境，一般用context名字来修饰，里面保存了web应用相关的一些设置和全局变量
2. `ServletContext`,是一个全局的储存信息的空间，服务器开始，其就存在，服务器关闭，其才释放。request，一个用户可有多个；session，一个用户一个；而`servletContext`，所有用户共用一个。所以，为了节省空间，提高效率，`ServletContext`中，要放必须的、重要的、所有用户需要共享的线程又是安全的一些信息；
3. 在 `SpringBoot` 中，context 有其继承体系：**每个不同的 `servlet` 都有自己独立的 `context`，而整个 application 有一个根 `context`，这个 `context` 是所有 `servlet` 所共享的** 

#### Application Events and Listeners

1. `Events` and `Listeners`[^1]

我们平时日常生活中也是经常会有这种情况存在，如：我们在平时拔河比赛中，裁判员给我们吹响了开始的信号，也就是给我们发布了一个开始的事件，而拔河双方人员都在监听着这个事件，一旦事件发布后双方人员就开始往自己方使劲。而裁判并不关心你比赛的过程，只是给你发布事件你执行就可以了。`listeners`监听`events`发生，然后采取一定动作.

2. `@Bean`[^2][^3]

  *In Spring, the objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container.* 

**IOC to solve**  Imagine an application with dozens or even hundreds of classes. Sometimes we want to share a single instance of a class across the whole application, other times we need a separate object for each use case, and so on.

 用来代替 XML 配置文件里面的 `<bean ...>` 配置 

what is spring bean[^4]

dependency injection[^5]

> 原来F 通过接口可以选择调用A,B,C中一个类得到F(X){X为A,B,C}，现在把F写道A,B,C类中，通过调用A,B,C得到F(X)。bean就是F

3. @component[^6]

 `@Component` is the most generic Spring annotation. A Java class decorated with `@Component` is found during classpath scanning and registered in the context as a Spring bean. `@Service`, `@Repository`, and `@Controller` are specializations of `@Component`, which are used for more specific cases. 

[^1]:  https://segmentfault.com/a/1190000011433514 
[^2]:  http://zetcode.com/springboot/bean/ 
[^3]:  https://zhuanlan.zhihu.com/p/46887997 
[^4]:  https://www.baeldung.com/spring-bean  
[^5]:  https://www.journaldev.com/2394/java-dependency-injection-design-pattern-example-tutorial
[^6]:  http://zetcode.com/springboot/component/

