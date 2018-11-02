---
title: java ee学习过程中使用到的一些函数与技巧(持续更新)
tags:
  - java ee
abbrlink: 4b57d472
date: 2018-10-23 15:51:43
---
### servlet用到的基础函数与技巧
servlet中获取传过来的url地址：request.getRequestUrl()
servlet中获取传过来的参数：request.getQueryString()

- servlet中的注解@WebFilter：
    此为filter注解，可以设置filtername，urlPattern，initParams(设置初始化值)
    例子：
    
    ```java
    @WebFilter(filterName="xxxxFilter",urlPatterns="/*",initParams={
        @WebInitParam(name="systemName",value="aaaa",
        @WebInitParam(name="version",value"2.0"
    }
    ```
    
### jsp中使用到的基础函数与技巧
如何让js获取当前页面input的id值
```jsp
<input value = "xxx" naem = "xxx" id = "xxx" onclick = "show(this)"></input>
<script type = "text/javascript">
function(o){
    var id = o.id;
}
```
