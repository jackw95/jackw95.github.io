---
layout: post
title:  "PHP - 字符串函数"
date:   2018-06-01
categories: PHP基础篇
excerpt: PHP基础
---

* content
{:toc}

#### 字符串常用函数

**获取字符串长度函数**

    /*
    * strlen函数
    * int strlen($var)
    * 获取字符串或数字的长度
    */
    $a = 'hello, woRld';
    $b = '王昭';  //utf8格式下，每个汉字3个字节长
    $c = 1111;
    echo strlen($a),"\n", strlen($b), strlen($c), "\n";

**大小写转换函数**

    /*
    * string strtolower(string $str)：字符串所有的字母转换为小写
    * string strtoupper(string $str)：字符串所有的字母转换为大写
    *
    * string ucfirst(string $str)：将字符串的首字母大写，其他字母不变
    * string ucwords(string $str)：将字符串中每个单词的首字母大写，其他字母不变
    *
    */
    $a = 'hello, world zhanGsan';
    echo strtolower($a), "\n";
    echo strtoupper($a), "\n";
    
    echo ucfirst($a), "\n";
    echo ucwords($a), "\n";

**字符串替换函数**

    //字符串替换函数
    /*
    * str_replace($search, $replace, $str)：实现字符串替换，区分大小写
    * str_ireplace($search, $replace, $str)：实现字符串的替换，不区分大小写
    *
    * $search：被替换字符串
    * $replace：替换字符串
    * $str：主字符串
    *
    */
    $a = 'this is a test';
    echo str_replace('is','is\'t', $a), "\n";
    echo str_ireplace('THIS', 'that', $a), "\n";
    
    //将'ZenD_CONTRollER_FronT'变成'Zend_Controller_Front'
    $str = 'ZenD_CONTRollER_FronT';
    $str = strtolower($str);
    $str = str_replace('_', ' ', $str);
    $str = ucwords($str);
    $str = str_replace(' ', '_', $str);
    echo $str, "\n";

**和html实体相关的函数**

    /*
    * htmlspecialchars函数
    * string htmlspecialchars(string $str)
    * 描述：预定义的字符转换为html实体
    *
    */
    $a = 'A>B, B<A';
    echo htmlspecialchars($a), "\n";

**删除空白或其他字符相关的函数**

    /*
    * ltrim函数
    * string ltrim(string $str[, string $charlist])
    * 描述：实现删除字符串开始位置的空格或其他字符
    * charlist规定从字符串中删除哪些字符，如果省略该参数，则移除所有的空白字符（空格、换行、回车等）
    *
    * rtrim函数
    * string rtrim(string $str[, string $charlist])
    * 描述：实现删除字符串结束位置的空格或其他字符
    *
    * trim函数
    * string trim(string $str[, string $charlist])
    * 描述：实现删除字符串开始和结束的位置的空格或者其他字符
    *
    */
    $a = '  ABC   ';
    echo $a, '长度为'.strlen($a), "\n";
    echo ltrim($a), '长度为'.strlen(ltrim($a)), "\n";
    echo rtrim($a), '长度为'.strlen(rtrim($a)), "\n";
    echo trim($a), '长度为'.strlen(trim($a)), "\n";

**字符串位置相关的函数**

    /*
    * strpos函数
    * int strpos(string haystack, mixed needle [,int offset])
    * 描述：将返回一个字符串在另一个字符串第一次出现的位置，区分大小写
    *
    * stripos函数
    * int strpos(string haystack, mixed needle [,int offset])
    * 描述：将返回一个字符在另一个字符第一次出现的位置，忽略大小写
    *
    * strrpos函数
    * int strrpos(string haystack, mixed needle [,int offset])
    * 描述：将返回一个字符串在另一个字符串最后一次出现的位置，区分大小写
    *
    * strripos函数
    * int strripos(string haystack, mixed needle [,int offset])
    * 描述：将返回一个字符串在另一个字符串最后一次出现的位置，忽略大小写
    *
    */
    $a = 'this is test';
    echo strpos($a, 'is'), "\n";
    //echo strpos($a,'Is'), "\n";
    var_dump(strpos($a,'Is'));  //不存在，返回false
    echo stripos($a,'Is'), "\n";  //忽略大小写，存在
    
    echo strrpos($a, 'is'), "\n";
    echo strripos($a,'Is'), "\n";

**字符串截取函数**

    /*
    * substr函数
    * string substr(string $str, int $start[, int $length])
    * 描述：截取字符串
    * 说明：如果省略length，则返回从start至字符串结尾之间的字符串
    *      如果startw为负数，则倒数，如果length为负数，表示从开始位置截取到结束位置
    *
    */
    $str = 'javascript';
    echo substr($str, 5), "\n";
    echo substr($str, 0, 5), "\n";
    echo substr($str, -5, 5), "\n";
    echo substr($str, -5,-2), "\n";
    
    //得到文件的扩展名
    $str = 'a.b.c.txt';
    $locate = strrpos($str, '.');  //获取最后一个点的位置
    echo substr($str, $locate+strlen('.')), "\n";  //截取点后面的字符串，即是拓展名

**字符串截取函数**

    /*
    * strstr函数
    * string strstr(string $haystack, mixed $needle)
    * 描述：将搜索一个字符串在另一个字符串中第一次出现的位置，然后返回字符串的其余部分，区分大小写
    *
    * stristr函数
    * string stristr(string $haystack, mixed $needle)
    * 描述：将搜索一个字符串在另一个字符串中第一次出现的位置，然后返回字符串的其余部分，忽略大小写
    *
    * strrchr函数
    * string strrchr(string $haystack, mixed $needle)
    * 描述：将搜索字符串在另一个字符串中最后一次出现的位置，然后返回字符串的其余部分，区分大小写
    *
    */
    $str = 'this Is a test';
    echo strstr($str, 'is'), "\n";
    echo stristr($str, 'is'), "\n";
    echo strrchr($str, 'is'),"\n";
    
    //得到文件的扩展名
    $str = 'a.b.c.txt';
    echo substr(strrchr($str, '.'), 1),"\n";

**反转字符串函数**

    /*
    * strrev函数
    * string strrev(string $string)
    * 描述：反转字符串
    *
    */
    $str = 'hello, world';
    echo strrev($str),"\n";

**字符串加密函数**

    /*
    * md5函数
    * string md5(string $str)
    * 描述：实现计算字符串的md5哈希值
    *
    * str_shuffle函数
    * string str_shuffle(string $str)
    * 描述：随机打乱字符串，可用于产生随机验证码
    */
    $str = 'imooc';
    echo md5($str),"\n";
    echo str_shuffle($str),"\n";

**分割字符串函数**

    /*
    * explode函数
    * array explode(string $delimiter, string $string[, int $limit])
    * 描述：使用一个字符串分割另一个字符串，返回一个数组，$limit限制数组内元素的个数
    *
    * implode函数
    * string implode(string $glue, array $pieces)
    * string implode(array $pieces)
    * 描述：将一个一维数组的值转化为字符串
    *
    */
    $str = 'this-is-a-test';
    $arr = explode('-', $str);
    print_r($arr);
    
    echo implode('-', $arr),"\n";  //使用'-'将数组内元素连接起来
    echo implode($arr),"\n";  //将数组内元素连接起来，功能和'.'相同

**格式化字符串函数**

    /*
    * sprintf函数
    * string sprintf(string $format[, mixed $args[, mixed $...]])
    * 描述：格式化字符串，和OC中NSLog(..)类似
    * 注意：如果%符号多于arg参数，则必须使用占位符，占位符位于%符号之后，由数字和"\$"组成
    *
    * $format参数，规定字符串以及声明变量的格式类型，取值为：
    * %%：返回一个百分号%
    * %b：二进制数
    * %d：包含正负号的十进制数（负数、0、正数）
    * %e：使用小写的科学计数法（例如：1.2e+2）
    * %s：字符串
    * %f：浮点数
    *
    * 附加的格式，必须放置在%和字母之间（例如%.2f）：
    * - + ：定义数字的正负
    * [0-9]：规定变量值的最小宽度
    * .[0-9]：规定小数位数或最大字符串长度
    *
    */
    $num = 5;
    $str = 'Tom';
    echo sprintf("this is %d test, %s", $num, $str),"\n";
    echo sprintf("this is %1\$s test, %1\$s", $str),"\n";
    echo sprintf("带两位小数：%1\$.2f 不带小数：%1\$d", $num),"\n";
