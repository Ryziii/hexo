---
title: java过滤器&&监听器
updated: '2018/10/25 17:33'
tags:
  - java web
abbrlink: '4e094881'
date: 2018-10-24 15:28:23
---
## 过滤器
过滤器是对web资源的请求拦截，完成特殊操作，尤其是对请求的预处理。
1. 应用场景
    - web资源权限访问控制
    - 请求字符集编码处理(中文字符)
    - 内容敏感字符词汇过滤
    - 相应信息压缩处理 

1. 过滤器生命周期
    - web应用程序启动时，web服务器创建filter的实例对象及初始化
    - 当请求访问与过滤器关联的web资源时，过滤器拦截请求，完成指定功能
    - Filter对象创建后会驻留在内存，在web应用移除或服务器停止时才销毁
    - init->doFilter->destroy

1. 过滤器实现步骤
    - 编写Filter接口，实现doFilter方法
    - 在web.xml文件中对filter类进行注册，并设置所拦截的资源

1. 过滤器链
    - 在一个web应用中，多个过滤器组合起来称之为一个过滤器链
    - 过滤器的调用顺序取决于过滤器在web.xml
    - 文件中的注册顺序(注册顺序决定的事过滤器预处理的调用顺序，响应后处理调用顺序是注册顺序的逆序  )

1. filter-mapping子元素dispatcheer
    - REQUEST(默认)
    - INCLUDE 需要在jsp中使用<jsp:include page="/xxx.jsp"/>
    - FORWARD 使用forward转发
    - ERROR 错误，需要定义error-page

## 监听器
可参照[这里](https://blog.csdn.net/yerenyuan_pku/article/details/52475065)
1. 按监听器对象分类：
    - ServletContext context上下文监听
    - HttpSession   回话监听
    - ServletRequest 请求对象监听
2. 按监听事件分类
    - 域对象自身的创建和销毁事件监听器(以生命周期)
        1. ServletContext->ServletContextListener
        2. HttpSession->HttpSessionListener
        3. ServletRequest->ServletRequestListener
    - 域对象中属性的创建、替换和消除事件监听器
        1. ServletContext->ServletContextAttributeListener
        2. HttpSession->HttpSessionAttributeListener
        3. ServletRequest->ServletRequestAttributeListener
    - 绑定在session中的某个对象的状态事件监听器(HttpSessionBindingListener)