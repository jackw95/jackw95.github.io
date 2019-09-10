---
layout: post
title:  "谈谈list()和each()"
date:   2019-04-16
categories: PHP基础
tags: php
excerpt: list()和each()的区别
---

* content
{:toc}

##### `list()`和`each()`
- `list()`
- `each()`

`list(mixed $varl[, mixed $...]) : array`
把数组中的值赋给一组变量。可以在单次操作内就为一组变量赋值，将索引数组下标为0的值赋值给变量1，下午1的赋值给变量2...

`array each(array &$array) : array`
返回数组中当前的键/值对并将数组指针向后移动一步。将传入的数组每个元素拆为一个新的数组，每执行一次操作一个元素，往后移动一位，执行到最后，返回`false`

```
//list()的功能，从左到右，一一对应索引数组从0开始的下标值
$arr1 = array('张三', '李四', '王五');
$arr2 = array(2=>'张三', 1=>'李四', '王五');
$arr3 = array('james'=>'詹姆斯', 'rose'=>'罗斯');

list($a1, $b1, $c1) = $arr1;
list($a2, $b2, $c2) = $arr2;

echo 'a1 = '.$a1.'<br/>'; //张三
echo 'b1 = '.$b1.'<br/>'; //李四
echo 'c1 = '.$c1.'<br/>'; //王五

echo 'a2 = '.$a2.'<br/>'; //Undefined variable... $a2找不到对应索引下标为0的值，所以没有赋值
echo 'b2 = '.$b2.'<br/>'; //李四
echo 'c2 = '.$c2.'<br/>'; //张三

echo "<pre/>";
var_dump(each($arr3)); //每读一次，数组指针向后移动一步
//0和key对应的是键，1和value对应的是值
/*
array(4) {
  [1]=>
  string(9) "詹姆斯"
  ["value"]=>
  string(9) "詹姆斯"
  [0]=>
  string(5) "james"
  ["key"]=>
  string(5) "james"
}
*/

var_dump(each($arr3));
/*
array(4) {
  [1]=>
  string(6) "罗斯"
  ["value"]=>
  string(6) "罗斯"
  [0]=>
  string(4) "rose"
  ["key"]=>
  string(4) "rose"
}
*/

var_dump(each($arr3)); //读到最后，没有值可以取，直接返回false

reset($arr3);
list($key, $value) = each($arr3);
echo $key.'----'.$value.'<br/>'; //james----詹姆斯
reset($arr3);

//通过each()和list()配合实现foreach一样的效果
while (list($key, $value) = each($arr3)) {
 echo $key.'----'.$value.'<br/>';
 //james----詹姆斯
 //rose----罗斯 
}
```


//计算数组的长度
`int count(mixed $变量)`








