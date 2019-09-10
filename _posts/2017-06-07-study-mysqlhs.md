---
layout: post
title:  "MySQL函数"
date:   2017-06-07
categories: MySQL
tags: mysql
excerpt: MySQL函数
---

* content
{:toc}

做项目的时候用数据库函数会方便很多，这样就不用每次取出来用php函数取遍历修改数据，这次有时间将常用的mysql数据库函数都整理了一下。

- 字符函数
- 数值运算符与函数
- 比较运算符与函数
- 日期时间函数
- 信息函数
- 聚合函数
- 加密函数

####字符函数
`CONCAT(str1,str2,...)`：字符串连接
`CONCAT_WS(separator,str1,str2, ...)`：使用指定的分隔符进行字符连接
`FORMAT(X,D)`：科学计数法数字格式化
`LOWER(str)`：转换成小写字母
`UPPER(str)`：转换成大写字母
`LEFT(str,len)`：获取左侧字符
`RIGHT(str,len)`：获取右侧字符
`LENGTH(str)`：获取字符串长度
`LTRIM(str)`：删除前导空格
`RTRIM(str)`：删除后续空格
`TRIM(str)`：删除前导空格和后续空格
`SUBSTR(str,pos,len)`：字符串截取
`[NOT] LIKE`：模式匹配（`%`表示0个或多个字符，`_`表示1个字符）
`REPLACE(str,from_str,to_str)`：字符串替换
注意：`php`中字符串截取从0开始，`sql`中从1开始

####数值运算符与函数
`CEIL(X)`：进一取整
`FLOOR(X)`：舍一取整
`ROUND(X,D)`：四舍五入保留D位小数
`POWER(X,Y)`：幂运算
`X DIV Y`：整除
`MOD(N,M)`：模运算（取余）
`TRUNCATE(X,D)`：数字截取（保留几位小数）

####比较运算符与函数
`[NOT] BETWEEN...AND...`：[不]在范围内
`[NOT] IN()`：[不]在列出值范围内
`IS [NOT] NULL`：[不]为空

####日期时间函数
`NOW()`：当前日期和时间
`CURDATE()`：当前日期
`CURTIME()`：当前时间
`DATE_ADD(date,INTERVAL expr unit)`：日期变化
`DATEDIFF(expr1,expr2)`：日期差值
`DATE_FORMAT(date,format)`：日期格式化
```
#一个月后的日期
select DATE_ADD(CURDATE(), INTERVAL 1 MONTH);  # 2019-08-26

#现在和一个月后的时间差值
select DATEDIFF(CURDATE(), DATE_ADD(CURDATE(), INTERVAL 1 MONTH));  # -31

#日期格式化
select DATE_FORMAT(NOW(), '%y/%m/%d');  # 19/07/26

```

####信息函数
`CONNECTION_ID()`：连接ID
`DATABASE()`：当前数据库
`LAST_INSERT_ID()`：最后插入记录的ID号
`USER()`：当前用户
`VERSION()`：当前数据库版本信息
`ROW_COUNT()`：当前影响的行数

####聚合函数
`AVG()`：平均值
`COUNT()`：计数
`MAX()`：最大值
`MIN()`：最小值
`SUM()`：求和

####加密函数
`MD5()`：MD5加密
`PASSWORD()`：密码算法
```
#修改当前mysql数据库的密码
> SET PASSWORD=PASSWORD('admin');
```

















