---
layout: post
title:  "Error"
date:   2018-04-16
categories: PHP基础
tags: php
excerpt: 自PHP 5.4.0起，实现了一种代码复用的方法
---

* content
{:toc}

在程序开发调试错误的过程中，我们总会遇到各种各样的`error`，部分`error`会影响到代码的执行，部分则只是给出一个`WARNING`或`NOTICE`，不会影响下面代码的继续执行。

**`PHP`中提供了一个错误控制运算符`@`，当将其放置在一个`PHP`表达式之前，该表达式可能产生的任何错误信息都被忽略掉。如果想控制输出错误的类型，可以通过`error_reporting()`函数来告诉编译器应该报何种错误。**

**`int error_reporting ([ int $level ] )`**：设置应该报告何种`PHP`错误
`$level`是错误级别，返回旧的 `[error_reporting]` 级别，或者在 `level` 参数未给出时返回当前的级别。
    <?php
    
    // 关闭所有PHP错误报告
    error_reporting(0);
    
    // Report simple running errors
    error_reporting(E_ERROR | E_WARNING | E_PARSE);
    
    // 报告 E_NOTICE也挺好 (报告未初始化的变量或者捕获变量名的错误拼写)
    error_reporting(E_ERROR | E_WARNING | E_PARSE | E_NOTICE);
    
    // 除了 E_NOTICE，报告其他所有错误
    error_reporting(E_ALL ^ E_NOTICE);
    
    // 报告所有 PHP 错误 (参见 changelog)
    error_reporting(E_ALL);
    
    // 报告所有 PHP 错误
    error_reporting(-1);
    
    // 和 error_reporting(E_ALL); 一样
    ini_set('error_reporting', E_ALL);
    
    ?>
错误的级别和常数是在`PHP`的预定义常量中定义的：

![clipboard.png](https://segmentfault.com/img/bVbdyo2?w=1074&h=910)

其中我们开发中常遇到的为`E_ERROR`，`E_WARNING`，`E_PARSE`，`E_NOTICE`。








