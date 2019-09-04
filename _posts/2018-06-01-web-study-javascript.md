---
layout: post
title:  "前端 - javascript"
date:   2018-06-03
categories: 前端
excerpt: 前端
---

* content
{:toc}

#### `javascript`简介

_`javascript`俗称`js`，`js`的正式名称是`ECMAScript`，是网景公司`Netscape`公司开发的一种基于客户端浏览器、基于面向对象、事件驱动式的网页脚本语言。主要用于：交互式操作，表单验证，网页特效，`web`游戏，服务器脚本开发等；_

**特点**

- `js`是一种解释性脚本编程语言 
- `js`是基于对象的脚本编程语言 
- 简单性 
- 安全性（不能访问本地硬盘） 
- 动态性的 
- 跨平台性（依赖浏览器，与操作系统无关） 

**三种使用方法** 

(1)使用`onclick`:属性构建执行`js`代码 

    <a href="#" onclick="alert(1)">点击</a>

(2)使用`<script../>`标签来包含`js`代码 

    <script type="text/javascript">
    	alert('Hello, world');
    </script>

(3)导入外部的`javascript`文件，让`html`页面和`js`脚本分离 

    <script src="outer.js" type="text/javascript"></script>

<hr />
####**`javascript`变量和数据类型**
`js`是弱类型脚本语言，使用变量之前，可以无需定义，当使用某个变量的时候直接使用即可。主要分为以下两种定义方式： 
(1)隐式定义：直接给变量赋值(隐式变量声明的时候必须赋初值) 
` a = 10;`
(2)显示定义：使用`var`关键字定义变量(使用之前必须赋初值，不然会报`undefined`错误) 
`var a = 10;`

**变量命名规则： **

- 首字母必须是字母、下划线或者`$`符号。 
- 余下的字母可以是下划线、`$`、任意字母或数字。 
- 变量名不能使用关键字 
- 变量名对大小写敏感。 

`js`是弱类型脚本语言，声明变量时无需指明变量的数据类型，`js`是解释时动态决定的，数据保存在内存中时也是有数据类型的，**常用数据类型**如下： 

- 数值类型(`number`)：包含整数和浮点数 
- 布尔类型(`boolean`)：只有`true`或`false`两个值 
- 字符串类型(`string`)：字符串必须用单引号或双引号括起来 
- 对象类型(`object`) 
- 数组类型（`array`）
- 未定义类型(`undefined`)：专门用来确定一个已经创建但是没有初值的变量 
- 空类型(`null`)：用来表明某个变量的值为空 
- `NaN`：非数值型


注：`undefined`和`null`的值相等，类型不同。 两个字符串是否相等，可用`==`来判断。

**数据类型转换： **

`+`号或者`toString()`：数值`number`类型转换成字符串 
`parseInt()`：将字符串转为整型 
`parseFloat()`：将字符串转换为浮点型 

**注意： **

`parseInt('67red') -> 67`(字符串转为整型的时候会自动截取前面的数字，后面的忽略)
`parseInt('red67') -> NaN`(字符串前面没有数字，会报`not a number`错误)

####**字符串常用方法：**

    stringObject.charAt(index)：获取字符串特定索引处的字符 
    index：下标(如果不在0～stringObject.length-1的范围内，返回'') 
    返回值：string

    stringObject.toUpperCase()：将字符串的所有字符转换成大写字母 
    返回值：string

    stringObject.toLowerCase()：将字符串的所有字符转换成小写字母 
    返回值：string

    stringObject.substring(start, end)：提取字符串中介于两个指定下标之间的字符 
    start：必须，字符串中开始位置 
    end：非必需，字符串中结束位置，如果不指定，会一直到字符串的结尾 
    返回值：string

    arrayObject.slice(start, end)：提取字符串中介于两个指定下标之间的字符，可指定负数 
    start：必须，字符串中开始位置 
    end：非必需，字符串中结束位置，如果不指定，会一直到字符串的结尾 
    返回值：string

    stringObject.indexOf(searchvalue,fromindex)：返回某个指定的字符串值在字符串中首次出现的位置 
    searchvalue：必须，需要查找的字符串 
    fromindex：非必须，字符串的指定位置，如果不指定，会从字符串的开始位置开始查找 
    返回值：number

    stringObject.replace(regexp/substr,replacement)：将字符串中的某个子串以特定的字符串替换 
    regexp/substr：需要替换的字符串 
    replacement：替换字符串的值 
    返回值：string

    stringObject.split(separator,limit)： 
    separator	必需，分隔符 
    limit 可选。该参数可指定返回的数组的最大长度，如果不指定，整个字符串都会被分割 
    返回值：string数组

    stringObject.concat(str1, str2...)：用于将多个字符串拼加成一个字符串 
    str1：字符串 
    返回值：string

**注意： **

- 用字符串做加法的时候，会做字符串拼接工作 
- 用字符串做减法、乘法、除法的时候，会将字符串转换成数值类型进行减法、乘法、除法运算


####**`js`数组**

三种定义数组的方法： 
(1)定义时直接给数组变量赋值 
`var arr = [1, 2, 3];`
(2)定义一个空数组 
`var arr = [];`
(3)用`new`方法定义数组 
`var arr = new Array();`

特点： 

- 数组长度可变 
- 同一数组中的元素类型可以互不相同 
- 当访问未赋值的数组元素时，该元素值为`undefined`，不会数组越界 

_`js`里面没有数组越界的概念，会显示`undefined`_

####**`js`运算符**

算术运算符：`+ - * / % ++ --`
赋值运算符：`=`
比较运算符：`> < >= <= == != === !==`
逻辑运算符：`&& || !`
位运算符：`& | ~ ^ << >>`
其他运算符：三目运算符(`?:`) 
`void`运算符：强行指定某个表达式的不会返回值
            `typeof` 运算符：获取某个变量的数据类型
    		 `instanceof`运算符：判断某个变量的数据类型是否为指定的数据类型
    		 `var a = void 3;  //输出为undefined`
    		 `document.write(typeof(str));  //输出为string`
    		 ` alert(arr instanceof Array);  //输出为true`

注意：`js`中没有继承的概念，所有的对象的父类都是`object`

####**`js`流程控制**

`js`支持的分支语句主要有`if`和`switch`语句。

    if(条件){
    	//表达式
    }else{
    	//表达式
    }

    //注意：switch中表达式的值可以是number类型，也可以是string类型
    switch(表达式){
    	case 值1: //表达式 break;
    	case 值1: //表达式 break;
    	...
    	default://表达式;
    
    }

`js`支持的循环语句主要有`while`循环，`do-while`循环，`for`循环，`for-in`循环

    //先判断，后执行
    while(循环条件){
    	//表达式
    }

    //先执行，后判断，至少执行一次
    do{
    	//表达式
    }while(循环条件)

    //当循环次数确定的情况下，一般用for循环，更简洁
    for(表达式1; 表达式2; 表达式3){
    	//表达式
    }

    //可用于遍历对象，比如数组(数组遍历的是下标，对象遍历的是属性，注意：都不是具体的值)
    for(变量 in 对象){
    	//表达式
    }

    //遍历的是下标
    var arr = [1, 2, 3, 4, 5];
    			arr[5] = 10;
    			arr[10] = 11;
    
    for(var a in arr){
    	document.write(arr[a]+'	');
    }

`js`提供了`break`和`continue`来改变循环的控制流

- `break`：跳出该层循环
- `continue`：结束该层循环的本次循环

常用的特殊语句

语句是`js`的基本执行单元，每条语句都是以分号结束，语句了前面的赋值语句、算术运算等语句之外，还有一些特殊语句。

- 语句块(包含在一对大括号里)
- 空语句(使用运用比较少)
- 异常抛出语句
    `throw new Error('异常抛出');`
- 异常捕捉语句
    ```
    try{
    	var age = 5;
    	if(age == 5){
    		throw new Error('异常抛出');
    	}
    }catch(e){
    	document.write('出错:'+e.message);
    }finally{
    	document.write('总会执行的finally块');
    }
    ```
