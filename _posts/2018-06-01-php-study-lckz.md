---
layout: post
title:  "PHP - 流程控制"
date:   2018-06-01
categories: PHP
excerpt: PHP语法
---

* content
{:toc}


#### 流程控制

**分支控制**

**`if`**

    echo "1. if"."\n";
    $a = 10;
    $b = 3;
    if ($a > $b){
        echo "a大于b"."\n";
    }

**`else`**：经常需要在满足某个条件时执行一条语句，而在不满足该条件时执行其他语句。

    echo "2. else"."\n";
    if ($a > $b){
        echo "a大于b"."\n";
    }
    else{
        echo "a不大于b"."\n";
    }

**`elseif`和`else if`**：两者的效果完全一致，但是如果用冒号来定义`if elseif`的条件，那就不能使用`else if`。

    echo "3. elseif"."\n";
    if ($a > $b){
        echo "a大于b"."\n";
    }
    elseif ($a == $b){
        echo "a等于b"."\n";
    }
    else{
        echo "a小于b"."\n";
    }
    
    //使用冒号的时候，必须得用elseif
    if ($a > $b):
        echo "a大于b"."\n";
    elseif ($a == $b):  //此情况下使用else if会报错
        echo "a等于b"."\n";
    else:
        echo "a小于b"."\n";
    endif;

**循环控制**

**`while`**：是`PHP`中最简单的循环类型，它和`c`语言中的`while`表现地一样。

    echo "4. while"."\n";
    while($a > 0):
        echo "$a\t";
        $a--;
    endwhile;

**`do-while`**：和`while`循环非常相似，`do-while`是先执行后判断，`while`是先判断后执行，相比之下，`do-while`至少执行一次。

    echo "\n5. do-while\n";
    do{
        echo "$a\t";
        $a++;
    }while($a < 10);
    echo "\n";

**`for`**：`for`循环是`PHP`中最复杂的循环结构。

    /*
     * 样式：
     * for(expr1; expr2; expr3){
     *      statement;
     * }
     * expr1：在循环开始前无条件执行一次
     * expr2：每次循环开始前时执行一次，用于判断该循环是否继续进行
     * expr3：每次循环结束后时执行一次
     * 上述三个都可以为空，如：
     * for(; ; ;){}
     * 当expr2为空时，默认为true，可无限循环。
     */
    echo "6. for\n";
    for ($i = 0; $i < 10; $i++)
    {
        echo "$i\t";
    }
    
    //可以使用: endfor;形式
    echo "\n";
    for ($i = 0; $i < 10; $i++) :
        echo "$i\t";
    endfor;

**`foreach`**：提供了遍历数组的简单方式，且仅仅能够用于数组和对象。

    /*
     *
     * 样式1：遍历给定的array_expression数组，每次循环中，当前单元的值被赋给$value并且数组内的指针向前移一步
     * foreach (array_expression as $value){
     *      statement;
     * }
     * 样式2：同上，不过除了当前单元的键名，也会在每次循环中赋值给$key
     * foreach (array_expression as $key => $value){
     *      statement;
     * }
     *
     * =>由于foreach依赖内部数组指针，在循环中修改其值将可能导致意外的行为。
     */
    echo "\n7. foreach\n";
    $arr = array(1, 2, 3, 4);
    foreach($arr as $value){
        echo $value."\t";
    }
    echo "\n";
    foreach($arr as $key=>$value){
        echo "key:$key => value:$value\t";
    }
    
    break：结束当前for,foreach,while,do-while或switch的结构的执行，跳出该层循环。
    continue：跳过该层循环的本次循环，执行下一次循环。
