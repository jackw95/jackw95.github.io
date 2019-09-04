---
layout: post
title:  "PHP - 数据类型"
date:   2018-06-01
categories: PHP
excerpt: PHP语法
---

* content
{:toc}

#### `PHP`数据类型
`PHP`支持八种原始的**数据类型**：

![clipboard.png](/img/bVbbDN4)


**布尔型**

    /*
     * boolean：TRUE FALSE
     * 以下值被认为是FALSE：
     * 布尔值FALSE本身
     * 整型值0（零）
     * 浮点型0.0（零）
     * 空字符串，以及字符串"0"
     * 不包含任何元素的数组
     * 特殊类型NULL（包括尚未赋值的变量）
     * ---所有其他值都被认为是TRUE
    */
    $foo = true;
    echo "foo的值是：$foo"."\n";
    
    if ($foo){
        echo "foo是真值"."\n";
    }
    else{
        echo "foo是假值"."\n";
    }

**整型**

    /*
     * Integer 整型，可以十进制、十六进制(0x)、八进制(0)、二进制(0b)
     * php不支持无符号整数，即php中的整数都是有符号的，最大的整数为PHP_INT_MAX
     * 注：如果给定一个数超出了integer的范围，将会被解释成float，同样如果执行的运算结果超出了integer范围，也会返回float
    */
    //PHP中没有整除运算符，1/2会产生float 0.5。
    echo 1/2;
    echo "\n";
    echo (integer)(1/2);  //integer强制转换为整型（去尾法）
    echo "\n";
    echo round(1/2);  //round()四舍五入
    echo "\n";
    //当从浮点型转换成整数时，将向下取整数（去尾法）
    echo (integer)0.8;  //输出：0
    echo "\n";

**浮点型**

    /*
     * Float：浮点数
     * 永远不要直接比较两个浮点数是否相等
     * 要测试浮点数是否相等，要使用一个仅比该数值大一丁点的最小误差值。
    */
    $a = 1.234;
    $b = 1.235;
    echo "\n";

**字符串**

    /*
     * string：字符串
     * 一个string就是由一系列的字符组成，每个字符等同与一个字节。
     * string可以用4中方式表达：
     * 单引号：单引号内的字符串中的变量和特殊字符的转义序列不会被替换。
     * 双引号：会对变量和转义字符进行替换。
     * heredoc结构：
     * nowdoc结构
     *
     * 字符串细节：
     * 一个字符串就是由一系列的字符组成，因此：
     * 一个字母         占一个字节
     * 一个数字         占一个字节
     * 汉字(gbk/gb2312) 占两个字节
     * 汉字(utf-8)      占三个字节
     */
    
    //heredoc格式
    /*
     * 使用注意：
     * 1. <<<固定 AAA名称可以变化，一般来说全部大写
     * 2. <<<标识符 后面不能带任何内容，包括空格
     * 3. 结束的标识符前面不能有空格
     * 4. heredoc可以解析变量和转义字符
     */
    $str = <<<AAA
    FDSAJFKLDASJFKLD;AJF;DASJFK;DASKF\nJD;KLSAFJKDLS;ANFDSAJFLKDS;A
    AAA;
    echo $str;

**数组**

    /* Array：PHP中的数组是一个有序映射，映射是一种把values关联到keys的类型。 
     * -->array可以接受任意数量用逗号分割的健值对。
     * PHP可以同时包含integer和string类型的键名。
     * key：可以是一个整数integer或字符串string。
     * value：可以是任意类型的值。
     *
     * 1. 包含有合法整型值的字符串会被转换为整型（如"8"会被转换为8，但是"08"不能转换为8）
     * 2. 浮点数会被转换为整型，意味着小数部分会被舍去。
     * 3. 布尔值会被转换为整型。
     * 4. NULL会被转换为空字符串，即""。
     * 5. 数组和对应不能被用为键名。
     *
     * 如果数组定义中多个单元都用了同一个键名，则只会使用最后一个，之前其他的都会被覆盖。
    */
    echo "\n";
    $arr1 = array(
        "key1" => "value1",
        "key2" => "value2"
    );
    var_dump($arr1);
    
    echo "\n";
    $arr2 = array(
        1 => "a",
        2.2 => "b",
        true => "c"  //会对之前key为1的进行覆盖
    );
    
    //echo $arr2; echo不能直接对数组进行输出
    var_dump($arr2);
    echo "\n";
    
    //如果对给出的值没有指定键名，则取当前最大的整数索引值，则新的键名将是该值+1，如果指定的键名已经有值，则该值会被覆盖。
    //所以key为可选项，如果未指定，PHP将自动使用之前用过的最大的integer键名+1作为新键名，最小值为0，如果当前还没有整数索引，键名为0
    $arr2[] = 4;
    var_dump($arr2);
    echo "\n";
    
    $arr3 = array(
        "a",  //键值为0
        "b",  //键值为1
        6 => "c",
        "d"   //键值为7
    );
    var_dump($arr3);
    echo "\n";
    
    //访问数组：可以用array[key]语法访问，也可以使用array{key}
    $arr4 = array(
        "key1" => "value1",
        "key2" => "value2"
    );
    var_dump($arr4["key1"]);
    echo "\n";
    var_dump($arr4{"key1"});
    echo "\n";
    
    $arr5 = array(5 =>1, 4 => 2);  //数组的创建
    var_dump($arr5);
    echo "\n";
    
    $arr5[] = 3;  //添加一个新的key-value对
    var_dump($arr5);
    echo "\n";
    
    $arr5["x"] = 5;  //如果x存在，则覆盖value，如果不存在，添加
    var_dump($arr5);
    echo "\n";
    
    unset($arr5[4]);  //移除该键值对
    var_dump($arr5);
    echo "\n";
    
    unset($arr5);  //移除整个数组
    //            var_dump($arr5);
    echo "\n";
    
    //注意：这里所使用的最大整数键名不一定就是当前数组中，它只要在上次数组重新生成索引后曾经存在过就行了。
    $arr6 = array(1, 2, 3, 4, 5, 6);
    print_r($arr6);
    echo "\n";
    foreach ($arr6 as $i => $value){  //遍历数组，移除所有元素
    //                echo $value;
    //                echo "<br/>";
        unset($arr6[$i]);
    }
    print_r($arr6);  //此时数组为空
    echo "\n";
    
    $arr6[] = 9;  //此时添加一个key-value（注意键名为6，不为0）
    print_r($arr6);
    echo "\n";
    
    $arr6 = array_values($arr6);  //重新索引
    $arr6[] = 10;  //此时key为1，上一个key为0
    print_r($arr6);
    echo "\n";
    
    //unset()函数允许删除数组中的某个键值对，但不会重新索引排序，如果需要删除后重建索引，可以用array_value()函数
    //foreach as 控制结构专门用于数组的，它提供了一个简单的方法来遍历数组
    
    //对于任意integer,float,string,boolean类型，如果将一个值转换为只有一个元素的数组（下标为0）
    $var = "你好";
    printf("%s", $var);
    //            var_dump(array($var));
    echo "\n";

**对象**

    /*
     *Object：对象，要创建一个新的对象object，使用new语句实例化一个类。
     *
    */
    class Foo
    {
        function  do_foo()
        {
            echo "doing foo.."."\n";
        }
    }
    
    $bar = new Foo();
    $bar -> do_foo();

**资源和`null`**

    /*
     * Resource资源类型：是一种特殊变量，保存了到外部资源的一个引用。
     *
     * NULL：表示一个变量没有值。
     * is_null()：判断一个变量是否为NULL。
     * unset()：移除。
     * 一个变量被认为NULL三种情况：
     * 被赋值为NULL。
     * 尚未被赋值。
     * 被unset()。
     *
     * mixed：说明一个参数可以接受多种不同的（但不一定是所有的）类型。
     *
     */