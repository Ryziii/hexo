---
title: xml和xpath
tags:
  - java web
abbrlink: 888f9884
date: 2018-10-16 10:46:54
---

1. xml允许使用实体引用表示特殊字符：![][image-1]`cdata:\<![CDATA[文本内容]]\>`

2. xml解析方式

   - DOM：Document Object Model：文档对象模型
   - SAX：Simple API for XML 行业闺房
   - JSXP：java API for XML：java解析xml文档的API

3. xpath

   xpath节点：

   ![][image-2]

   1. xpath基本关系：

	  - 基本值：没有父节点的子节点

	  - 项：一个项代表一个节点或基本值

	  - 序列：序列可以表示节点集(多个节点)或者项

   2. 节点关系：

	  - 父节点
	  - 子节点
	  - 兄弟节点
	  - 祖先节点
	  - 后代节点

   3. xpath相对路径绝对路径：xpath绝对路径以／开头，相对路径不以／开头

	  - /list/demo/xxx绝对路径
	  - list/demo/xxx相对路径

   4. xpath基础语法：xpath使用路径表达式定位xml文档中的节点和节点集

[image-1]:	https://ws1.sinaimg.cn/mw690/6bdd7ec4gy1fw9vgdb3ecj20yi0aedjr.jpg
[image-2]:	https://ws1.sinaimg.cn/mw690/6bdd7ec4gy1fw9wvumyntj214a0hwaoo.jpg