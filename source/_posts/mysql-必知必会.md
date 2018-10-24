---
title: 'mysql 必知必会'
date: 2018-10-22 15:38:47
tags:
    - mysql
---

### 第四章-mysql检索 限定
- SELECT：查询
- DISTINCT：去重
- LIMIT：限制查询条数。LIMIT 3 OFFSET 5（从第3行开始查询3个）
- 完全限定表名：`SELECT product.prod_name FROM crashcourse.products;`(从crashcourse数据库中查表名为product的列prod_name)

### 第五章-排序
1. ORDER BY：升序排列。
    - 使用方法：`SELECT prod_name FROM products ORDER BY prod_name;`
2. 多个列排序：
    - `SELECT prod_id,prod_price,prid_name FROM products ORDER BY prod_price,prod_name;`(先按产品价格后按照产品名即当产品价格相同时进行产品名排序)
3. 制定升\降序（DESC关键词）排列
    - 降序排列：`SELECT prod_id FROM products ORDER BY prod_id DESC;`
    - 升降序共用排序：`SELECT prod_id,prod_name FROM products ORDER BY prod_id DESC , prod_name;`(先按照prod_id降序排列，后按照prod_name升序)
    - ORDER BY位置：如果使用ORDER BY时，必须要在FROM之后，如果使用LIMIT，必须在ORDER BY之后。

### 第六、七章-过滤数据(where)
1. 简单使用：
    - `SELECT prod_name,prod_price FROM products WHERE prod_price = 2.50;`(返回prod_proce = 2.50的数据)
    - where子句操作符<img src="https://ws1.sinaimg.cn/large/6bdd7ec4gy1fwh3l84n2oj210s0h4jt0" width="90%" height="90%"/>
    - 范围检查：`SELECT prod_name,prod_price FROM products WHERE prod_price BETWEEN 5 AND 10;`
    - 检查NULL：`SELECT prod_name,prod_price FROM products WHERE prod_price IS NULL`
2. 组合WHERE子句：
    - AND操作符(可以过滤多个条件)：`SELECT prod_id,prod_price,prod_name FROM products WHERE prod_id = 1003 AND prod_price <= 10;`
    - OR操作符：`SELECT prod_name,prod_price FROM products WHERE prod_id = 1002 OR prod_id = 1003`(返回prod_id为1002**或者**1003的列)
    - OR AND共用，使用括号：`SELECT prod_price,prod_name FROM products WHERE (prod_id = 1002 OR prod_id = 1003) AND prod_price >= 10`
3. IN操作符：
    - 使用IN操作符和BETWEEN一样的功能：`SELECT prod_id FROM products IN (1002,1010);`
4. NOT操作符：取反

### 第八章-通配符过滤
1. LIKE操作符：使用LIKE说明指示mysql后的搜索模式利用通配符匹配而不是直接相等匹配
2. %通配符：表示匹配字符出现任意次数，有点像正则中的*
    - `SELECT prod_id,prod_name FROM products WHERE prod_name LIKE 'aaa%';`返回 aaa*
3. _通配符：匹配单个字符
4. 通配符速度很慢，很少使用，不应该放置在搜索模式的开始处。

### 第九章-使用正则
1. REGEXP：
    - `SELECT prod_name FROM products WHERE prod_name LIKE '1000' ORDER BY prod_name;`
    - `SELECT prod_name FROM products WHERE prod_name REGEXP '1000' ORDER BY prod_name;`
    - 上面两个一个使用LIKE一个使用REGEXP，使用LIKE的语句将不返回数据因为LIKE匹配的是整行，REGEXP匹配的是行内的值
    - REGEXP转义用 \\
    - 开始和结束符：^(开始)、$(结束)

### 第十章-计算字段
1. 