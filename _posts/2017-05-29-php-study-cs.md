---
layout: post
title:  "session与cookie"
date:   2017-05-29
categories: PHP基础
tags: php
excerpt: session与cookie概念
---

* content
{:toc}

#### `session`

**什么是`session`？**

 - `session`在计算机中，尤其在网络应用中，称为"会话控制"；具体到`web`中的`session`指的就是用户在浏览某个网站时，从进入网站到浏览器关闭所经过的这段时间，也就是用户浏这个网站所花费的时间。因此从上述的定义中可以看到，`session`是一个特定的时间概念。

**为什么要使用`session`？**

 - `HTTP`协议是一种无状态的协议，即同一个客户端的本次请求和上次请求没有对应关系，http服务器并不知道这两个请求来自同一个客户端；优点在于减轻服务器的压力，缺点在于每次请求会传输大量重复的内容信息
 -  `session`提供在`PHP`脚本中定义全局变量的方法，使得这个全局变量在同一个session中对于所有的`PHP`脚本文本内都有效。所以，`session`是基于`HTTP`服务器的用于保持状态的方法；
 -  `session`允许通过将数据存储到`HTTP`服务器中，以在整个用户会话过程中保持该数据；所以，`session`不仅是一个时间概念，还包括了特定的用户和服务器；

**`session`的工作原理**    
    
 - 会话由一个唯一标识符标识，可使用`session_id`函数读取此标识符。为`PHP`应用程序启用会话状态时，将检查应用程序中每个页面请求是否有浏览器发送的`sessionID`值。如果未提供任何`sessionID`值，则`PHP`将启动一个新会话，并将该会话的`sessionID`值随响应一起发送到浏览器。
 - 默认情况下，`sessionID`值存储在`cookie`中，也可以实现在`URL`中存储`sessionID`
   只要一直使用相同的`sessionID`值来发送请求，会话就被视为活动的，如果特定会话的请求间隔超过指定的超时值（以秒为单位），则该会话被视为已过期。如果使用过期的`sessionID`值发送的请求将生成一个新的会话

**和`session`相关的函数**

    /*
     * session_start
     * 描述：启动新会话或者重用现有会话
     * 语法：bool session_start([array $options = []])
     * ---在服务器上创建了一个sessionID，并创建了一个存储session的文件
     * 说明：
     * A. $options参数是一个关联数组，如果提供的话，则会用其中的项目覆盖"会话配置"中的配置选项；
     * B. 如果通过GET或者POST方式，或者使用cookie提交了会话ID，则会重用现有会话
     *
     * session_id
     * 描述：获取/设置当前会话ID
     * 语法：string session_id([string $id])
     * 说明：
     * A. 如果指定$id参数的值，则使用指定值作为会话ID
     * B. 如果设置$id参数的值，必须在调用session_start()函数之前调用session_id()函数
     *
     * session_name
     * 描述：读取/设置会话名称
     * 语法：string session_name([string $name])
     * 说明：
     * A. 如果指定$name参数，session_name()函数会更新会话名称，并返回原来的会话名称；
     * B. 如果指定$name参数，必须在调用session_start函数之前调用session_name()函数
     *
     * session_destroy
     * 描述：销毁一个会话中的全部数据
     * 语法：bool session_destroy()
     *
     * chrome浏览器cookies存储地：
     * ~/Library/Application Support/Google/Chrome/Default/Cookies
     * 将Cookies加扩展名sqlite，然后用sqlite工具打开Cookies
     */
    

**`PHP`配置中`session`片段**

    /*
     * 在/Applications/XAMPP/etc/php.ini文件中可以查看下列片段：
     *
     * session.auto_start(boolean)
     * 描述：session.auto_start指定会话模块是否在请求开始时自动启动，默认为0（不启动），一般不进行修改该配置；
     *
     * session.name(string)
     * 描述：指定会话名以用做cookid的名字，只能由字母数字组成，默认为'PHPSESSID';
     *
     * session.save_handler(string)
     * 描述：定义用来存储和获取与会话关联的数据的处理器的名字，默认为files，即文件；
     *
     * session.save_path(string)
     * 描述：定义传递给存储处理器的参数，如果选择默认的files文件处理器，则值则是文件的路径；
     *
     * session.gc_maxlifetime(integer)
     * 描述：指定过了多少秒之后数据就会被视为"垃圾"并被清除；
     *
     * session.gc_probability(integer)、session.gc_divisor(integer)
     * 描述：定义在每个会话初始化时启动gc进程的概率，此概率通过gc_probability/gc_divisor计算，值为1000，表示为千分之一
     *
     */



#### `cookie`

**什么是`cookie`？**

- `HTTP cookie`也叫`Web cookie`或者浏览器`cookie`，是服务器发送到用户浏览器并保存在浏览器上的数据，它会在浏览器下一次发起请求时被携带并发送到服务器上；
- `HTTP cookie`是`HTTP`标头的组成部分；
- `session`是存储在服务器端，`cookie`是存储在浏览器端

**`cookie`的作用**

 1. 会话状态管理（如用户登录状态、购物车）：如十天自动登录
 2. 个性化设置（如用户自定义设置）
 3. 浏览器行为跟踪（如跟踪分析用户信息）

**与`cookie`相关的函数**

    /*
     * setcookie函数
     * 描述：设置cookie
     * 语法：bool setcookie(string $name[, string $value = ""[, int $expire = 0[, string $path = ""[, string $domain = ""]]]])
     * 说明：
     * A. $name参数用于指定cookie名称；
     * B. $value参数用于设置cookie值；
     * C. $expire参数用于设置cookie的生命周期（Unix时间戳）；
     * D. $path参数用于设置服务器上可用cookie的路径；如果设置为"/"，则代表在整个域名内都有效，
     *    如果设置为"/foo/"，则仅代表在域名内的/foo目录及其子目录内有效；
     * E. $domain参数用于设置cookie可用的域名范围（包含子域名）；
     *
     * 注意：会话期cookie是指浏览器关闭之后会被自动删除，也就是它仅在会话期间有效；
     *      会话期cookie不需要指定过期时间(Expire)；
     *
     * 持久cookie：指定一个特定的过期时间(Expire)；
     *
     */





