---
title: Spring学习-Bean装配专题
date: 2018-10-25 16:33:49
tags:
    - Spring
---
## Bean配置项
- Id：唯一标识
- Class：具体要实现的那个类
- Scope：作用域
- Constructor arguments：构造器参数
- Properties：属性
- Autowiring mode：自动装配模式
- lazy-initialization mod：懒加载模式
- Initialization/destruction method：初始化和销毁方法

## Bean的作用域
- singleton：单例，指一个Bean容器中只在一份
- prototype：每次请求(每次使用)创建新的实例，destroy不生效
- request：每次http请求创建一个实例仅在当前request内有效
- session：同上，每次http请求创建，当前session有效
- global session：基于portlet的web中有效（portlet定义了global session），如果在web中，同session

## Bean的生命周期
1. 初始化，Bean的初始化有两种方法
    1. 配置xml文件中的init-method
    2. 实现org.springframework.beans.factory.InitializingBean接口，并覆盖afterPropertiesSet方法
2. 销毁
    1. 配置xml中的destory-method
    2. 实现org.springframework.beans.factory.DisposableBean接口，覆盖desroty方法
3. 全局默认初始化、销毁方法
    1. 在xml文件中在beans里添加`default-init-method="init" default-destory-method="destory"` 
    2. 当使用接口或配置xml进行初始化和销毁时，全局默认方法失效
    
覆盖接口方法先于xml配置文件调用

## Aware是什么
Spring中提供了一些以Aware为结尾的接口，实现了Aware接口的beean在呗初始化之后，可以获取相应的资源，即对Spring相应资源的操作。 

## Bean自动装配(Autowiring)
有byType、byName和construct(byType和construct寻找的是类型，和bean id没有关系)三种方法在xml中配置

## Resources
针对于资源文件的统一接口
- UrlResource：URL对应的资源，根据一个URL地址即可构建
- ClassPathResource：获取类路径下的资源文件
- FileSystemResource：获取文件系统里面的资源
- ServletContextResource：ServletContext封装的资源，用于访问ServletContext环境下的资源
- InputStreamResource：针对于输入流封装的资源
- ByteArrayResource：针对于字节数组封装的资源
- ResourceLoader
    ![](https://ws2.sinaimg.cn/large/006tNbRwgy1fwlrr6h4b3j31680gitcj.jpg) 