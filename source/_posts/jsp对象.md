---
title: jsp内置对象
tags:
  - java web
abbrlink: ba1c11f7
date: 2018-10-15 09:34:07
---

1. **request：**
   - 封装了由web浏览器和其他客户的生成的HTTP请求的细节(参数，属性，头标和数据)
   - 作用域：用户的请求周期
   - 作用域：可以在相邻两个web资源之间共享一个，使用：setAttribute和getAttribute
   - 请求转发(跳转)：getRequestDispatcher.forward(request,response);
2. **out：**输出流对象
3. **response：**封装了返回到HTTP客户端的输出，给页面作者提供设置响应头标和状态码的方式
4. **pageContext：**
   - 请求转发：pageContext.forward
   - include方法
   - pageContext可以获取其他的内置对象。getRequest、getResponse 
   - 作用域：当前页面
5. **session：**
   - 作用域：会话期间
   - 有效周期：session.setMaxInactiveInterval(int second)
6. **error：**

   - exception对象只能在错误页面中使用
   - 有一个页面出现了错误页面进入指定错误处理页面，在<%@page中使用errorPage指定error.jsp
7. **application：**
   - 提供关于服务器版本，应用级初始化参数和应用内资源绝对路径方式
   - 作用域：web容器生命周期
   - 可用于访问量