---
layout: post
title:  数学函数"
date:   2017-05-24
categories: PHP基础
tags: php
excerpt: PHP基础
---

* content
{:toc}

#### 数学函数库

**进一、舍一取整，四舍五入**

    /*
     * floor函数
     * float floor(float $value)
     * 描述：将实现舍一取整
     *
     * ceil函数
     * float ceil(float $value)
     * 描述：将实现进一取整
     *
     * round函数
     * float round(float $value[, int $precision=0])
     * 描述：实现四舍五入的功能，$precision表示保留几位小数
     *
     */
    $a = 9.75;
    $b = 5.3;
    echo floor($a), "\n";  //9
    echo ceil($a), "\n";   //10
    echo round($a,1), "\n";  //9.8
    echo round($a), "\n";  //10
    echo round($b), "\n";  //5

**幂运算和平方根**

    /*
     * pow函数
     * number pow(number $base, number $exp)
     * 描述：幂指数运算
     *
     * sqrt函数
     * float sqrt(float $arg)
     * 描述：平方根
     *
     */
    $num = 3;
    echo pow(3, 2), "\n";
    echo sqrt($num), "\n";

**最大值和最小值**

    /*
     * max函数
     * mixed max(mixed $value, mixed $value,...)
     * 描述：返回最大值
     *
     * min函数
     * mixed min(mixed $value, mixed $value,...)
     * 描述：返回最小值
     *
     */
    echo '最大值: ', max(10,5,3,90,12), "\n";
    echo '最小值: ', min(10,5,3,90,12), "\n";

**随机数**

    /*
     * rand函数
     * int rand(int $min, int $max)
     * 描述：产生随机数
     *
     * mt_rand函数
     * int mt_rand(int $min, int $max)
     * 描述：产生一个更好的随机数，比rand函数的执行速度更快
     *
     *
     * 可用于产生随机验证码
     *
     */
    echo rand(1, 10), "\n";
    echo mt_rand(1, 10), "\n";
    
    //产生4位随机验证码
    $chars = 'abcdefghijklmnopqrstuvwxyz';
    
    for ($i=0; $i<4; $i++)
    {
        static $char = '';
        $num = mt_rand(0,25);
        $char .= substr($chars,$num,1);  //使用变量之前必须先赋值
    }
    echo $char, "\n";

**数字格式化**

    /*
     * number_format函数
     * string number_format(format $number[, int $decimals = 0])
     * 描述：将以千位分隔符方式格式化数字,$desimals表示保留到小数点的几位
     *
     */
    $num = 10000000.00;
    echo number_format($num,1), "\n";

**浮点数余数**

    /*
     * fmod函数
     * float fmod(float $x, float $y)
     * 描述：将返回除法的浮点数余数，%取余只会进行整数的余数操作
     *
     */
    $num = 5.27;
    echo $num%2, "\n";
    echo fmod($num, 2), "\n";
