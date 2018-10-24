---
title: java ee学习过程中使用到的一些函数与技巧(持续更新)
date: 2018-10-23 15:51:43
tags:
---
### servlet用到的基础函数与技巧
servlet中获取传过来的url地址：request.getRequestUrl()
servlet中获取传过来的参数：request.getQueryString()
### jsp中使用到的基础函数与技巧
如何让js获取当前页面input的id值
```jsp
<input value = "xxx" naem = "xxx" id = "xxx" onclick = "show(this)"></input>
<script type = "text/javascript">
function(o){
    var id = o.id;
}
```