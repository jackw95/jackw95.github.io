---
layout: post
title:  "PHP操作MySQL"
date:   2017-06-02
categories: PHP基础
tags: php
excerpt: PHP操作MySQL的三种方式
---

* content
{:toc}

####`PHP`操作`MySQL`

**`PHP`操作`MySQL`的三种方式：**
- `MySQL`：非永久连接，性能比较低，`PHP5.5`以后废弃；
- `MySQLi`：永久连接，减轻服务器压力，只支持`MySQL`；
- `PDO`：能实现`MySQLi`的常用功能，支持大部分数据库；



**`PHP`扩展查看函数**：`phpinfo();`
**`php`配置文件**：`php.ini`



**`MySQL`方式连接数据库**

    //设置html的字符集
    header('content-type:text/html;charset=utf-8');
    
    //连接数据库
    $server = '127.0.0.1';
    $username = 'root';
    $password = '123';
    $port = '3309';
    $link = mysql_connect("{$server}:{$port}", $username, $password);
    
    //选择数据库
    $db_name = 'test005';
    mysql_select_db($db_name);
    
    //设置字符集
    $charset = 'utf8';
    mysql_set_charset($charset);
    
    /*
     * MySQL方式执行SQL语句
     * mysql_query()对insert, update, delete, drop之类的操作，执行成功时返回true, 出错时返回false
     */
    $query = '';
    mysql_query($query);
    
    $query_insert = 'INSERT INTO users(id, name, salary) VALUES(1, \'张三\', 3000)';
    $query_update = 'UPDATE user SET name =\'李四\' WHERE id = 1';
    $query_delete = 'DELETE FROM users WHERE id = 1';
    $query_drop = 'DROP TABLE IF EXISTS user';
    
    mysql_query($query_insert);
    
    /*
     * mysql_query()对SELECT操作，执行成功会返回一个resource，如果查询出现错误则返回FALSE
     * 返回的结果资源应该传递给mysql_fetch_array($result)和其他函数来处理结果表，取出返回的数据
     * 参数：MYSQL_ASSOC MYSQL_NUM和MYSQL_BOTH
     */
    $query_select = 'SELECT * FROM users';
    $result = mysql_query($query_select);
    
    $line_row = mysql_fetch_row($result);  //索引数组，第一条数据
    $line_assoc = mysql_fetch_assoc($result);  //关联数据，第一条数据
    $line_array = mysql_fetch_array($result);   //混合数组，既有关联数组，又有索引数组，第一条数据
    
    //遍历
    while ($line = mysql_fetch_assoc($result)){
        $data[] = $line;  //每一次取出的结果集都添加到$data数组中
    }
    var_dump($data);  //输出所有的结果集
    
    //关闭数据库连接
    mysql_close($link);

**`MySQLi`面向过程方式操作数据库**

    /****** 面向过程 ******/
    
    //连接数据库
    $host = '127.0.0.1';
    $user = 'root';
    $password = '123';
    $database = 'test005';
    $port = '3309';
    $connect = mysqli_connect($host, $user, $password, $database, $port);
    
    //执行SQL语句
    $query = 'SELECT * FROM user';
    $result = mysqli_query($connect, $query);
    
    mysqli_fetch_row($result);        //索引数组，第一条数据
    mysqli_fetch_assoc($result);      //关联数据，第一条数据
    mysqli_fetch_array($result);      ////混合数组，既有关联数组，又有索引数组，第一条数据
    
    var_dump(mysqli_fetch_assoc($result));
    
    //获取结果集
    var_dump(mysqli_fetch_all($result));
    
    //关闭数据库连接
    mysqli_close($connect);





