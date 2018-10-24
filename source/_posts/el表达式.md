---
title: EL表达式和JSTL
date: 2018-10-18 16:12:28
tags:
	- java web
---

1. - EL表达式：Expression Language（表达式语言），目的是替代JSP页面中的复杂代码。

   - EL表达式语法：
   
        ${变量名}

   - 当session和request作用域的变量名冲突了，可以使用el名称sessionScope.username和requestScope.username

   ![](https://ws1.sinaimg.cn/mw690/6bdd7ec4gy1fwchaje6d3j20q009wwhk.jpg)

   - 当通过封装的类传输时可以使用三种方法(假定User类)

     1. ${user.username}

        ${user.password}

     2. ${requestScope.user.username}

        ${requestScope.user.password}

     3. ${user['username']}

        ${user['password']}

1. JSTL
   - JSTL：JSP标准标签库(JavaServerPages Standard Tag Library)

   - JSTL通常会和EL表达式合作实线JSP页面编码
   
   - 使用JSTL需要在JSP中添加taglib指令:

    ```jsp 
    <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
    ```

