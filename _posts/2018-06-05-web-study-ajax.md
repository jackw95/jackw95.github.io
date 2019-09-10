---
layout: post
title:  "Ajax"
date:   2018-06-05
categories: Web前端
tags: web
excerpt: 异步JavaScript和XML，是一种用于创建快速动态网页的技术。
---

* content
{:toc}

###`Ajax`
**`Ajax`**全称**`Asynchronous Javascript And XML`**（异步`JavaScript`和`XML`），是一种用于创建快速动态网页的技术。它在不重载全部网页页面的情况下，实现了对部分网页的更新。

**`ajax`请求和浏览器地址请求区别**
- 浏览器发起的请求，请求结果展示在浏览器上
- `ajax`发起的请求，结果保存在`js`变量里

**适用场景**
- 注册用户时，对用户名的唯一性进行验证
- 发送手机验证码
- 只要是不刷新网页，收发数据的情况，`ajax`都是不错的选择

**语法：`$.ajax([settings])`**
常备参数
- `url` ：发送请求的地址
- `type`：请求方式，值为`GET`,`POST`，默认为`GET`
- `data`：发送到服务器的数据
- `async`：请求类型，值为`true`,`false`，分别代表异步和同步，默认为`true`
- `dataType`：预期服务器返回的数据类型，可用值`xml`, `html`, `json`, `text`等
- `success`：`Function()`，请求成功后的回调函数
- `error`，`Function()`，请求失败后的回调函数
- `timeout`：设置请求超时时间（毫秒）
注：当`dataType`为`json`，即返回值类型为`json`的情况下，`ajax`获取到的值是`object`类型

**`ajax`中需要注意的问题：**
**跨域问题**
说到跨域，必须得理解同源的概念，同源：两个页面地址中的协议、域名和端口号都相同。而跨域则是源A中的代码去请求源B中的数据，由于安全方面的原因，客户端`js`使用`XMLHttpRequest`只能同源访问，跨域访问会出错。（暂不提如何解决跨域问题）

**`ajax`调试**
进入`Chrome`控制台
点击`network`
- `headers`：在`request headers`中可以看到发送的数据
- `response`：服务器返回的内容 
选中`XHR`：`XML HTTP Request`，表示由`ajax`发起的请求

###关于`JSON`
**`JSON`**全称**`JavaScript Object Notation`**，`JS`对象简谱，是一种轻量级的数据交换格式。
**语法：**
- 对象表示为键值对
- 数据由逗号分隔
- 花括号保存对象
- 方括号保存数据

**`JSON`和`JS`对象的关系**
`JSON`是`JS`对象的字符串表示法，它使用文本表示一个`JS`对象的信息，本质是一个字符串。

    var obj = {a: 'Hello', b: 'World'};   //js对象    
    var json = "{'a': 'Hello', 'b': 'World'}";  //JSON字符串

**`JSON`和`JS`对象互转**
要实现从对象转换为`JSON`字符串，使用`JSON.stringify()`方法：
    var json = JSON.stringify({a: 'Hello', b: 'World'});  //结果是"{'a': 'Hello', 'b': 'World'}"

要实现从`JSON`转为对象，使用`JSON.Parse()`方法：
    var obj = JSON.parse("{'a': 'Hello', 'b': 'World'}");  //结果是{a: 'Hello', b: 'World'}

**`JSON`和`PHP`对象互转**
    $str = json_encode($obj);    //对象转JSON字符串
    $obj = json_decode($json);    //JSON字符串转对象



