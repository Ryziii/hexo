---
title: servlet笔记、转发与重定向
date: 2018-10-16 17:29:49
tags:
	- java web
---

Servlet:servlet是用来处理用户请求的小程序

response.setContentType("text/html;charset=UTF-8"); 目的是为了控制浏览器的行为，即控制浏览器用UTF-8进行解码；

response.setCharacterEncoding("UTF-8");目的是用于response.getWriter()输出的字符流的乱码问题

1. 如果中文返回出现？？字符，这表明没有加response.setCharacterEncoding("UTF-8");
2. 如果返回的中文是“烇湫”这种乱码，说明浏览器的解析问题，应该检查下是否忘加response.setHeader("Content-type", "text/html;charset=UTF-8");





![](https://ws1.sinaimg.cn/mw690/6bdd7ec4gy1fwa7wcvxdij21fs0imagt.jpg)

service服务负责转发doget或dopost或doxxx方法，如果重写了service就需要添加上转发方法

![](https://ws1.sinaimg.cn/mw690/6bdd7ec4gy1fwahjurj68j21160gq46j.jpg)

![](https://ws1.sinaimg.cn/mw690/6bdd7ec4gy1fwahkaq3k8j21e40oowmo.jpg)

servletContext表示整个javaweb工程

servletConfig表示某一个servlet中的配置文件  

转发和重定向：
- 转发：request.getRequestDispatcher("目标地址").forward(request,response);
- 重定向：response.sendRedirect("目标地址");
1. 转发调用HttpServletRequest，重定向调用HttpServletResponse
2. 使用转发不会改变浏览器地址栏的url，转发前后url一样；重定向会改变浏览器url。
3. 转发只请求一次服务器，重定向请求服务器两次。