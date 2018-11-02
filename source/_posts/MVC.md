---
title: MVC开发流程与文件上传笔记
tags:
  - java web
abbrlink: 88f3c71a
date: 2018-10-17 15:03:11
---

![](https://ws1.sinaimg.cn/mw690/6bdd7ec4gy1fwb8ennb3ij21a40o611k.jpg)

文件上传jsp要素

1. form表单必须是post提交方式
2. 表单必须有文件上传项，文件上传必须有name属性和值
3. 表单的enctype属性必须设置为multipart/form-data

文件上传种servlet中的操作

1. 创建一个工厂资盘文件项工厂对象
2. 创建一个核心解析类
3. 解析request请求，返回的是List集合，List集合中存放的事Fileitem对象
4. 遍历集合，获得每个FileItem，判断表达项还是文件上传项目
