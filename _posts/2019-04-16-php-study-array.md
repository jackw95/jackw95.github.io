---
layout: post
title:  "常用数组函数"
date:   2019-04-16
categories: PHP基础
tags: php
excerpt: 常规函数、指针操作
---

* content
{:toc}

##### 常规函数
- `array_shift()`
- `array_unshift()`
- `array_push()`
- `array_pop()`
- `array_rand()`

##### 指针操作
- `current()`
- `key()`
- `next()`
- `prev()`
- `reset()`
- `end()`

`array_shift(array &$array) : mixed`
将数组开头的单元移出数组。将`array`的第一个单元移除并作为结果返回，将`array`的长度减一并将其他单元向前移动一位。所有数字键名将改为从0开始计数，文字键名不变。

`array_unshift(array &$array [, mixed $...])`
在数组开头插入一个或多个单元。将传入的单元插入到`array`数组的开头，单元是作为整体被插入的，因此传入单元将保持同样的顺序。所有数字键名将修改为从0开始计算，文字键名不变。

`array_push(array &$array, mixed $value1 [, mixed $...]) : int`
将一个或多个单元压入数组的末尾（入栈）。将`array`当作一个栈，并将传入的变量压入array的末尾，`array`的长度将根据入栈变量的数组增加。

`array_pop(array &$array) : mixed`
弹出数组的最后一个单元（出栈）。弹出并返回`array`数组的最后一个单元，并将数组`array`的长度减一

`array_rand(array $array [, int $num = 1]) : mixed`
从数组中随机取出一个或多个单元，并返回随机条目的一个或多个键。

`current(array &$array) : mixed`
返回数组中的当前单元。每个数组中都有一个内部的指针指向它“当前的”单元，初始指向插入到数组中的第一个单元

`key(array $array) : mixed`
从关联数组中取出键名。返回数组中当前单元的键名

`next(array &$array) : mixed`
将数组中的内部指针向后移动一位，行为和`current()`类似，但是是内部指针向后移动一位

`prev(array &$array) : mixed`
将数组中的内部指针向前移动一位

`reset(array &$array) : mixed`
将数组中的内部指针指向第一个单元

`end(array &$array) : mixed`
将数组中的内部指针指向最后一个单元
