---
title: HF jsp 第三章
tags:
  - head first JSP&Servlet
abbrlink: 6bb10f0c
date: 2018-09-04 11:46:01
---

1.  在”servlet把请求转发给jsp“和“jsp从请求对象得到问答”的过程中，需要注意在servlet中的setAttribute和jsp中的getAttribute两个的变量需要一样。coding过程中在set的时候写的是sytles在get中写的是style，寻了会儿bug。
2. Parameter和Attribute
   - Parameter没有setParameter，Attribute有。
   - 一般的在两个Web组建为链接关系时使用getParameter()方法获得请求参数(从表单获取时使用)
   - 两个Web组建为转发关系时使用getAttribute()来获取转发源组建共享request范围内的数据(常用语servlet传数据到jsp，用在request的属性)