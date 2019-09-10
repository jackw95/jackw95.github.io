---
layout: post
title:  "谈谈empty()和isset()"
date:   2019-04-16
categories: PHP基础
tags: php
excerpt: empty()和isset()的区别
---

* content
{:toc}

##### 关于`FALSE`
当转换为`boolean`时，以下值被认为是`false`
- 布尔值`false`本身
- 整型值`0`（零）
- 浮点值`0.0`
- 空字符串`''`，字符串`'0'`，以及尚未赋值的变量
- 不包含任何元素的数组
- 特殊类型`NULL`
所有其他值都被任务是`TRUE`

##### `NULL`类型的三种情况：
1、通过变量赋值明确指定变量的值为`NULL`
2、一个变量没有给任何值
3、使用函数`unset()`将变量销毁掉

#### `empty()`和`isset()`函数的区别
- `empty()`可以向括号中间传入一个变量，这个变量的值如果为`false`或者`null`的话，返回`true`
- `isset()`可以向括号中间传入一个或者多个变量，变量与变量间用逗号分开。只要有一个变量为`null`，则返回`false`，否则，则返回`true`

`unset()`函数的功能是销毁变量，`unset(变量)`括号中间插入想要毁掉的变量名，这个变量就会被销毁。
