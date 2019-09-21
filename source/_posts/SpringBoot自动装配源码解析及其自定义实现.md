---
title: SpringBoot自动装配源码解析及其自定义实现
date: 2019-07-19 22:55:44
tags:	
	- springboot
	- 源码分析
---
# SpringBoot自动装配源码解析及其自定义实现
## 前言
我们都知道spring框架最大的好处就是ioc控制反转，同时带的弊端就是配置文件写法高度麻烦👎。特别是在使用框架且在不知道框架源码的内容情况下，这些配置文件显得有点行尸走肉，成为一种负担，为了写而写，不写框架根本跑不起来。

在SringBoot的诞生之后，这种状况有了改善。

- starter简化依赖配置
- 自动装配

这两点给我们的使用带来了质的飞跃👍，不用漫无头脑的复制配置文件、优雅的管理项目！

所以这篇文章将带你了解如下内容

1. springboot如何简化依赖配置
2. springboot自动装配原理
3. 如何让自己的项目自动装配进springboot里面

## 简化依赖
利用如下maven配置就能轻松SpringMVC的依赖问题

```
<!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-web -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>2.1.6.RELEASE</version>
</dependency>
```
这其实就是利用了maven的继承，maven也像java一样可以继承，这一句简单的依赖就实现了spring-boot-starter-web.pom里面所有的依赖。

## 自动装配
首先我们看springboot的@SpringBootApplication这个注解，它包括了@EnableAutoConfiguration这个注解，然后我们在进入@EnableAutoConfiguration这里面看，它又有@Import({EnableAutoConfigurationImportSelector.class})这个东西。

ps：@Import注解把用到的bean导入到了当前容器中，这里是EnableAutoConfigurationImportSelector

好了，这就是重中之重，EnableAutoConfigurationImportSelector的这个方法实现了自动装配
```java
protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
List<String> configurations = SpringFactoriesLoader.loadFactoryNames(this.getSpringFactoriesLoaderFactoryClass(), this.getBeanClassLoader());
        Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you are using a custom packaging, make sure that file is correct.");
        return configurations;
    }
```

我们跟踪这个当法，找到了如下内容

![路径发现](https://i.loli.net/2019/07/18/5d301b020003540626.png)

它利用了classLoader.getResources("META-INF/spring.factories")加载所的spring.factories，于是我们打开一个factories看看

```
Auto Configure
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
org.springframework.boot.autoconfigure.admin.SpringApplicationAdminJmxAutoConfiguration
```
说明这个factories文件指明了各种java形式的配置文件。
于是我们就进入这个`SpringApplicationAdminJmxAutoConfiguration`里面看看他有什么东西

![屏幕快照 2019-07-18 下午3.17.40.png](https://i.loli.net/2019/07/18/5d301d30c241362832.png)


是的 他就是典型的java配置文件@Bean与@Configuration的组合，取代了xml的配置文件。

总结：
我们看到了，都是框架作者的功劳啊，他帮我们都写好了依赖文件，springboot通过classloader加载到了这些依赖文件，注入到了框架。这些过程对于我们来说都是透明的，所以我们只用@Autowired就有想要的东西了。

## 给自己的框架加入自动装配
这里暂时没空写了，参考这位dalao的吧，实测能跑通
[SpringBoot自动装配之写一个Starter](https://juejin.im/post/5d284e9cf265da1bcb4f590c#heading-0)