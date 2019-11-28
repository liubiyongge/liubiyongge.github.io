---
layout:     post
title:      "Spring boot annotation"
subtitle:   ""
date:       2019-11-22
author:     "LiuBiyongge"
header-img: "img/in-post/Web.png"
tags:

  - Java Web
---



# Spring boot annotation

[TOC]

## spring boot annotation[^1]

### `@EnableAutoConfiguration`

Spring Boot会根据使用`@EnableAutoConfiguration`批注添加到项目中的依赖项(添加的JAR依赖项)自动配置应用程序。 例如，如果MySQL数据库在类路径上，但尚未配置任何数据库连接，则Spring Boot会自动配置内存数据库。

### `@SpringBootApplication`

spring boot应用程序的入口点是包含`@SpringBootApplication`注释和`main`方法的类。`@SpringBootApplication`注释包括自动配置，组件扫描和Spring Boot配置。`@SpringBootApplication`注释包括所有其他注释

### `@ComponentScan`

Spring Boot使用`@ComponentScan`注释自动扫描项目中包含的所有组件。Spring Boot应用程序在应用程序初始化时扫描所有bean和包声明。`@ComponentScan`注释用于查找`bean`以及使用`@Autowired`注释注入的相应内容。

### `@SpringBootConfiguration`

### `SpringBoot 组件`

### `@RestController@Controller`[^4]
都是注册一个rest应用(也就是一个页面), `@RestController`是`@ResponseBody`和`@Controller`的组合注解
### `@ResponseBody`


### `@AutoWired`  

annotation we inject our `AppName` bean into the field.

```
    @Autowired
    private AppName appName;
```


​		any method annotated with `@Autowired` is a config method. It is called on bean instantiation after field injection is done. The arguments of the method are injected into the method on calling.

### `@Bean@ Configuration`[^5][^7][^8]   

execute that method and register the return value as a bean within a `BeanFactory`. By default, the bean name will be the same as the method name,@Configuration可理解为用spring的时候xml里面的`<beans>`标签 @Bean可理解为用spring的时候xml里面的`<bean>`标签

```
  @Bean
   public RestTemplate getRestTemplate() {
      return new RestTemplate();   
   }
```

```
    @Autowired
    RestTemplate restTemplate;

    @Bean
    public  RestTemplate getRestTemplate(){
        return new RestTemplate();
    }
    注册一个类RestTemplate的bean, 然后@Autowired找到他赋值给restTemplate
```

### `@RequestBody`

注释用于定义请求正文内容类型。

```java
public ResponseEntity<Object> createProduct(@RequestBody Product product) {
}
```

### `@RequestParam`

`@RequestParam` annotation used for accessing the query parameter values from the request. Look at the following request URL:

```
http://localhost:8080/springmvc/hello/101?param1=10&param2=20
```

In the above URL request, the values for `param1` and `param2` can be accessed as below:

```
public String getDetails(
	@RequestParam(value="param1", required=true) String param1,
        @RequestParam(value="param2", required=false) String param2){
...
}
```

The following are the list of parameters supported by the `@RequestParam` annotation:

**defaultValue –** This is the default value as a fallback mechanism if the request is not having the value or it is empty.

**name –** Name of the parameter to bind

**required –** Whether the parameter is mandatory or not. If it is true, failing to send that parameter will fail.

**value –** This is an alias for the `name` attribute

### `@RequestMapping`

`@RequestMapping`注释用于定义访问REST端点的Request URI。可以定义Request方法来使用和生成对象。默认请求方法是:`GET`。

```java
@RequestMapping(value = "/products")
public ResponseEntity<Object> getProducts() { }
```

###  `@PathVariable`

`@PathVariable` identifies the pattern that is used in the URI for the incoming request. Let’s look at the below request URL:

```
http://localhost:8080/springmvc/hello/101?param1=10&param2=20
```

The above URL request can be written in your [Spring MVC](https://javabeat.net/spring-boot-spring-mvc/) as below:

```
@RequestMapping("/hello/{id}")
	public String getDetails(@PathVariable(value="id") String id,
	@RequestParam(value="param1", required=true) String param1,
	@RequestParam(value="param2", required=false) String param2){
.......
}
```

The `@PathVariable` annotation has only one attribute `value` for binding the request URI template. It is allowed to use the multiple `@PathVariable` annotation in the single method. But, ensure that no more than one method has the same pattern.

While developing [RESTful Web Services](https://javabeat.net/spring-4-rest-example/), it will be useful to use this annotation for forming the more flexible URI (Also Read : [REST API Best Practices](https://javabeat.net/rest-api-best-practices/)).

### `@Component`



###  异常处理 

#### `@ControllerAdvice`  

 是一个注解，用于全局处理异常。 

#### `@ExceptionHandler`

 用于处理特定异常并将自定义响应发送到客户端 

### `@Component`[^9]

 A Java class decorated with `@Component` is found during classpath scanning and registered in the context as a Spring bean, 如 `Spring Boot拦截器`, ` Spring Boot Servlet过滤器 ` 

###  `@Data` 

是 lombok 的注解，自动生成Getter，Setter，toString，构造函数等 

### 服务组件

####  `@Service` 

服务组件(Service Components)是包含`@Service`注释的类文件。 这些类文件用于在不同的层中编写业务逻辑，与`@RestController`类文件分开。 此处显示了创建服务组件类文件的逻辑

## RestTemplate[^10]

SpringRestTemplate是Spring 提供的用于访问 Rest 服务的客端, RestTemplate提供了多种便捷访问远程Http服务的方法，能够大大提高客户端的编写效率,所以很多客户端比如Android或者第三方服务商都是使用RestTemplate 请求 restful服务

## 补充

- spring bean vs java bean[^6]

spring bean已经被实例化

- REST[^2]

REST 指的是一组架构[约束条件](https://baike.baidu.com/item/%E7%BA%A6%E6%9D%9F%E6%9D%A1%E4%BB%B6)和原则。满足这些约束条件和原则的应用程序或设计就是 RESTful。

RESTFUL特点包括：

1、每一个URI代表1种资源；

2、客户端使用GET、POST、PUT、DELETE4个表示操作方式的动词对服务端资源进行操作：GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源，DELETE用来删除资源；

3、通过操作资源的表现形式来操作资源；

4、资源的表现形式是XML或者HTML；

5、客户端与服务端之间的交互在请求之间是无状态的，从客户端到服务端的每个请求都必须包含理解请求所必需的信息。

- restful api[^3]

restful api 用url描述资源,用Http方法描述行为，用Http状态码描述不同的结果,使用json作为交互数据(包括入参和响应)

- 源码结构

```
com
    +- yiibai
        +- myproject
            +- Application.java
            |
            +- model
            |    +- Product.java
            +- dao
            |    +- ProductRepository.java
            +- controller
            |    +- ProductController.java
            +- service
            |    +- ProductService.java
```

---

`@Service` `@Bean`都可以理解为spring bean, 都可被@AutoWired发现

[^1]: spring boot 中文教程 https://www.yiibai.com/spring-boot/spring_boot_introduction.html 
[^2]: restful 百科https://baike.baidu.com/item/RESTful/4406165
[^3]: restful api https://www.jianshu.com/p/320cee90391f
[^4]: Control and RestControl的区别 https://www.jianshu.com/p/c816eb1c6711 
[^5]: sping boot bean 讲解 http://zetcode.com/springboot/bean/
[^6]: https://www.yiibai.com/spring-boot/spring_boot_beans_and_dependency_injection.html#article-start
[^7]: spring bean http://wiki.jikexueyuan.com/project/spring/bean-life-cycle.html
[^8]: spring bean reference https://docs.spring.io/spring-javaconfig/docs/1.0.0.M4/reference/html/ch02s02.html
[^9]: http://zetcode.com/springboot/component/  
[^10]: https://dpb-bobokaoya-sm.blog.csdn.net/article/details/90668738

