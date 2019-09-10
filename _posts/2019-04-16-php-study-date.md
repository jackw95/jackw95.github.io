---
layout: post
title:  "Date"
date:   2018-04-16
categories: PHP基础
tags: php
excerpt: 日期相关的概念和函数
---

* content
{:toc}

##### 时间的三个概念：
- 时区
 全球分为24个时区，中国采用北京所在地东八区的时间作为全国统一使用的时间
- 世界时
以格林尼治（英国某地区）的地方时间为准，英文简称`GMT`
- `unix`时间戳
从`unix纪元`（1970年1月1日零时）开始到一个时间经过的秒数

默认时区函数
`string date_default_timezone_get(void)`
`bool date_default_timezone_set(string $timezone_identifier)`

//获取当前的`unix`时间戳
`time()`

//将一个时间戳进行格式化输出，`$format：Y m d H m s`
`string date(string $format[, int $timestamp])`

//获取当前系统的时间数组
`array getdate([int $timestamp = time()])`

//判断一个输出的日期是否有效，常用与用户提交的表单数据验证
`boolean checkdate(month, day, year)`

//将英文文本的日期时间描述解析为`unix`时间戳
`int strtotime(string $time[, int $now = time()])`
`echo strtotime("+1 week 2 days 4 hours 2 seconds");`

//能够返回当前`unix`时间戳和微秒数，参数为`true`的话，将会返回一个浮点类型的时间，否则返回的是一个字符串。常用与计算函数的执行效率
`mixed microtime([bool $get_as_float])`






