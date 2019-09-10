---
layout: post
title:  "日期函数"
date:   2017-05-26
categories: PHP基础
tags: php
excerpt: 日期时间函数
---

* content
{:toc}
#### 日期时间函数

**格式化日期**

    /*
     * date函数
     * string date(string format[, int timestamp])
     * 描述：格式化一个本地时间/日期
     *
     * format格式：
     * Y：4位数字完整表示的年份
     * y：2位数字表示的年份
     * F：月份，完整的文本格式
     * M：三个字母缩写表示的月份
     * m：数字表示的月份，有前导零
     * n：数字表示的月份，没有前导零
     * d：月份中的第几天，有前导零
     * j：月份中的第几天，没有前导零
     * l：星期几，完整的文本格式
     * D：星期中的第几天，文本表示，3个字母
     * w：星期中的第几天，数字表示
     * H：小时，24小时格式，有前导零
     * i：有前导零的分钟数
     * s：秒数，有前导零
     *
     */
    echo date('Y-m-d H:i:s'), "\n";  //2018-01-17 05:55:53

**与时区相关的函数**

    /*
     * date_default_timezone_set函数
     * bool date_default_timezone_set(string timezone_identifier)
     * 描述：设置默认时区
     *
     * date_default_timezone_get函数
     * string date_default_timezone_get()
     * 描述：获取默认时区
     *
     * 亚洲
     * Asia/Hong_Kong
     * Asia/Shanghai
     *
     * 配置文件修改：
     * php.ini中date.timezone中设置值，然后重启Apache即可
     *
     */
    echo date_default_timezone_get(), "\n";  //Europe/Berlin
    
    date_default_timezone_set('Asia/Shanghai');
    echo date('Y-m-d H:i:s'), "\n";  //2018-01-17 12:55:53
    echo date_default_timezone_get(), "\n";  //Asia/Shanghai

**Unix时间戳**

    /*
     * Unix时间戳
     * 称为Unix时间，是一种时间表示方法，定义为格林威治时间1970年01月01日00时00分00秒
     * 起到现在的总秒数。Unix时间戳不仅被使用在Unix系统，类Unix系统中，也在许多其他操作
     * 系统中被广泛应用。
     *
     * time函数
     * int time()
     * 描述：返回当前Unix时间戳
     *
     * strtotime函数
     * int strtotime(string $time[, int $now = time()])
     * 描述：将字符串转换成Unix时间戳
     *
     * 以"天"为基础的格式
     * yesterday  昨天午夜
     * midnight  午夜
     * today  今天
     * noon  中午12:00:00
     * tomorrow  明天午夜
     * first day of ??  某月第一天
     * last day of ??  某月最后一天
     *
     * 一天的时间戳：24*24*60 = 86400
     *
     * microtime函数
     * mixed microtime([bool $get_as_float])
     * 描述：返回当前Unix时间戳和微秒数，bool为true表示返回当前带微秒的时间戳
     *
     * ---可用于计算程序运行的时间
     */
    echo time(), "\n";  //当前的时间戳
    echo strtotime('-3 month'), "\n";  //获取之间的时间戳
    echo microtime(true), "\n";

**生成唯一的ID**

    /*
     * uniqid函数
     * string uniqid(string $prefix =""[, bool $more_entropy = false])
     * 描述：生成唯一ID，$prefix是前缀
     */
    echo uniqid(), "\n";
    echo uniqid(time()), "\n";
    
    //常见uuid生成方式
    echo md5(uniqid(microtime() . mt_rand())), "\n";

**获取日期、时间信息**

    /*
     * getdate函数
     * array getdate([int timestamp])
     * 描述：可以获取日期、时间信息
     *
     */
    print_r(getdate());
    
    /*
    Array
    (
        [seconds] => 5
        [minutes] => 55
        [hours] => 15
        [mday] => 17
        [wday] => 3
        [mon] => 1
        [year] => 2018
        [yday] => 16
        [weekday] => Wednesday
        [month] => January
        [0] => 1516175705
    )
     */


