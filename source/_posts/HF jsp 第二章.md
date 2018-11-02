---
title: HF jsp 第二章
tags:
  - head first JSP&Servlet
abbrlink: 26afac5e
date: 2018-08-30 11:18:03
---


1. 为什么MVC三端分离了又要使用统一的控制器管理多个MODEL和VIEW，MODEL负责不同的业务逻辑（如购物车的状态），VIEW是视图
2. 容器为web应用提供了通信支持，生命周期管理、多线程支持、生命方式安全、以及jsp支持，这样就可以分离不同功能，全身心投入业务逻辑的开发
3. 容器创建一个相应对象和请求对象，servlet可以用这些对象得到相关的请求信息，并传信息给客户
4. HTTP响应![image-20180830224958085](https://ws1.sinaimg.cn/mw690/6bdd7ec4gy1fv8cgh0v8rj213q0vkaqe.jpg)
5. CGI模式的动态web![image-20180830224806221](https://ws1.sinaimg.cn/mw690/6bdd7ec4gy1fv8ch39wv8j20wg0yutmn.jpg)
6. 典型的servlet是拓展了一个HttpServletRequest类并覆盖了一个或者多个服务方法（doPost()   doGet()），分别对应于浏览器调用的HTTP方法
7. 可以使用servlet mapping映射serlvet类到url来完成请求servlet，部署名和可以和实际的类名完全不同
8. 
![image-20180903235415834](https://ws1.sinaimg.cn/mw690/6bdd7ec4gy1fv8che5icej21560n44ky.jpg)



