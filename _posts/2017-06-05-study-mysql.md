---
layout: post
title:  "MySQL学习"
date:   2017-06-05
categories: MySQL
tags: mysql
excerpt: 按照数据结构来组织、存储和管理数据的仓库
---

* content
{:toc}

####什么是数据库？
_数据库`Database`是按照数据结构来组织、存储和管理数据的仓库。常见的数据库有`Oracle`、`DB2`、`SQL Server`、`MySQL`等..._

`MySQL`是一个关系型数据库管理系统，开源免费，由瑞典`MySQL AB`公司开发，目前属于`Oracle`旗下产品。

**相关术语**
`DB(Database)`：数据库是存储数据的集合。
`DBS(Database System)`：数据库系统，由数据库和数据库管理软件组成。
`DBMS(Database Management System)`：数据库管理系统，是操作和管理数据库的一个系统。
`SQL(Structured Query Language)`：结构化查询语言，是数据库的程序设计语言


**`MySQL`相关命令行操作**

    配置文件：my.cnf
    登录信息中需要注意的：
    ---命令行需要以';'或者是'\g'结尾，不然无法结束；
    ---可以通过'help'或者'\h'或者'?'加上相关关键字来查看手册；
    ---'\c'可以取消当前命令的执行；
    
	mysql -uroot -p[密码]			#登录MySQL
    mysql -uroot -p -D db_name	  #登录MySQL的同时打开数据库
    exit;						#退出MySQL
    quit;						#退出MySQL
    \q;							#退出MySQL
    ctrl+c						#退出MySQL
    
    #获取当前MySQL的版本号
    mysql -V;
    mysql --version;
    
**`SQL`语句语法规范**

- 常用`MySQL`的关键字需要大写，库名、表名、字段名称等使用小写；
- `SQL`语句支持折行操作，拆分的时候不能把完整单词拆开；
- 数据库名称、表名称、字段名称不能使用`MySQL`的保留字，如果必须要使用，需要用反引号；

**常用`SQL`语句**
`SELECT USER();`			#得到登录的用户
`SELECT VERSION();`		#得到MySQL的版本信息
`SELECT NOW();`			#得到当前的日期时间
`SELECT DATABASE();`		#得到当前打开的数据库

**`SQL`的注释**

    #注释内容
    --注释内容

**数据库`SQL`操作**

    #创建数据库
    CREATE DATABASE|SCHEMA [IF NOT EXISTS] db_name;
    CREATE DATABASE|SCHEMA [IF NOT EXISTS] db_name DEFAULT CHARACTER SET [=] 'charset'; #指定编码格式
    --注意：数据库名称最好有意义，名称不要包含特殊字符或者是MySQL关键字。
    
    #修改数据库的编码方式
    ALTER DATABASE db_name DEFAULT CHARACTER SET [=] 'charset';
    
    #删除数据库
    DROP DATABASE [IF EXISTS] db_name;
    
    #打开指定数据库
    USE db_name;	#在操作数据库里面的表之前需要先打开数据库
    
    #SHOW方法
    SHOW DATABASES|SCHEMAS;		   				 #查看全部的数据库
    SHOW CREATE DATABASE db_name;				 #查看数据库的详细信息（编码格式）
    SHOW WARNINGS;				   				#查看上一步操作产生的警告信息
    
    
    #MySQL注释
    '#'注释内容
    '--'注释内容

**数据表`SQL`操作**
_数据库表是一系列二维数组的集合，用来代表和存储数据对象之间的关系，是数据库最重要的组成部分之一。_
**数据保存在表中，表名要求唯一，不要包含特殊字符，最好含义明确**
	
- 主键：指的是一个列或多列的组合，其值能唯一地标识表中的每一行，一个表中只能有一个主键。主键主要是用于其他表的外键关联，以及本记录的修改与删除。
- 外键：如果公共字段在一个表中是主键，那么这个字段被称为另一个表的外键，一个表中可以有多个外键。外键保持数据一致性和完整性，主要目的是控制存储在外键表中数据，使两张表形成关联，外键只能引用外表中的列的值或者使用空值。
- 索引：对表中一列或者多列的值进行排序的一种结构，使用索引可快速访问表中的特定信息，一个表中可以有多个索引。索引的主要目的是加快检索表中数据的方法。

表结构相关操作：
```
#创建表
CREATE TABLE[IF NOT EXISTS] table_name（ 
   字段名称1 字段类型[完整性约束条件],
   字段名称2 字段类型[完整性约束条件],
   ...
）ENGINE=存储引擎 CHARSET=编码方式;
    
#删除表
DROP TABLE [IF EXISTS] table_name;
    
#查看表的创建信息
SHOW CREATE TABLE table_name;
    
#查看当前数据库下所有的表
SHOW [FULL] TABLES [{FROM|IN} db_name];
    
#查看表结构
DESC table_name;					  
DESCRIBE table_name;
SHOW COLUMNS FROM table_name;
    
#添加字段
ALTER TABLE table_name ADD 字段名称 字段属性[完整性约束条件] [FIRST|AFTER 字段名称]; 
    
#删除字段
ALTER TABLE table_name DROP 字段名称;
    
#添加默认值
ALTER TABLE table_name ALTER 字段名称 SET DEFAULT 默认值;
    
#删除默认值
ALTER TABLE table_name ALTER 字段名称 DROP DEFAULT;
    
#修改字段类型、字段属性
ALTER TABLE table_name MODIFY 字段名称 字段类型[字段属性] [FIRST|AFTER 字段名称]
    
#修改字段名称、字段类型、字段属性
ALTER TABLE table_name CHANGE 原字段名称 新字段名称 字段属性 [FIRST|AFTER 字段名称]
    
#添加主键
ALTER TABLE table_name ADD PRIMARY KEY(字段名称)
    
#删除主键
ALTER TABLE table_name DROP PRIMARY KEY;
    
#添加唯一
ALTER TABLE table_name ADD UNIQUE KEY|INDEX [index_name](字段名称)  --如果不添加index_name，则索引名称默认为字段名称
    
#删除唯一
ALTER TABLE table_name DROP INDEX index_name;
    
#修改数据表名称
ALTER TABLE table_name RENAME [TO|AS] new_table_name;
RENAME TABLE table_name TO new_table_name;
```
 
**关键字含义**
`UNSIGNED`：无符号，没有负数，从0开始
`ZEROFILL`：零填充，当数据显示长度不够的时候可以使用前补0的效果填充至指定长度
`NOT NULL`：非空约束，也就是插入值的时候这个字段必须要给值
`DEFAULT`：默认值，如果插入记录的时候没有给字段赋值，则会使用默认值
` PRIAMARY KEY`：主键，标识记录的唯一性，值不能重复，一个表只能有一个主键
`UNIQUE KEY`：唯一性索引，一个表中可以有多个字段是唯一索引，同样的值不能重复，但是NULL除外
`AUTO_INCREASE`：自动增长，只能用于数值列，而且配合索引或主键使用
`FOREIGN KEY`：外键约束
`COMMENT`：添加注释
    
    #设置主键的两种方式
    CREATE TABLE test_primarykey(id INT UNSIGNED PRIMARY KEY, username VARCHAR(20));		#直接在字段后面设置属性
    CREATE TABLE test_primarykey1(id INT UNSIGNED, username VARCHAR(20), PRIMARY KEY(id));	 #利用函数设置字段

**`MySQL`数据类型**

- 数值型
    - 整数型`TINYINT` `SMALLINT` `MEDIUMINT` `INT` `BIGINT` `BOOL/BOOLEAN`
    - 浮点数`FLOAT` `DOUBLE` `DECIMAL`
    - 定点数
- 字符串类型`CHAR(M)` `VARCHAR(M)` `TINYTEXT` `TEXT` `MEDIUMTEXT` `LONGTEXT` `ENUM('', ''...)` `SET('', ''...)`
- 日期时间类型

**`CHAR`和`VARCHAR`的比较：**
`CHAR`是定长，`VARCHAR`变长；
`CHAR`效率高于`VARCHAR`，`CHAR`相当于拿空间换时间，`VARCHAR`拿时间换空间；
`CHAR`默认存储数据的时候，后面会用空格填充到指定长度，而在检索的时候会去掉后面空格，`VARCHAR`不会进行填充，检索的时候尾部的空格会留下。
注意：`TEXT`类型的字段不能有默认值，检索的时候不存在大小写转换。


**`MySQL`中常用函数**
`COUNT()`语法：
`COUNT(column_name)`：返回指定列的值的数目
`COUNT(*)`：返回表中的记录数目
`COUNT(DISTINCT column_name)`：返回指定列的不同值的数目
    
`CONCAT()`语法：
`CONCAT()`：用于将多个字符串连接成一个字符串。
用法：`CONCAT(str1, str2, …)`，返回结果为连接参数产生的字符串，如果任何一个参数为`NULL`，则返回为`NULL`
`CONCAT_WS()`：用一个分隔符将多个字符串连接成一个字符串
用法：`CONCAT_WS(separator, str1, str2, …)`，如果分隔符为`NULL`，则返回为`NULL`


**`MySQL`存储引擎**
`MyISAM`存储引擎

- 默认`MyISAM`的表会在磁盘中产生三个文件：`.frm` `.MYD` `.MYI`
- 可以在创建表的时候指定数据文件和索引文件存储位置
- `MyISAM`单表最大支持的数据量2的64次方条记录
- 每个表最多可以建立64个索引
- 如果是复合索引，每个复合索引最多包涵16个列，索引值最大长度是1000B
- `MyISAM`引擎的存储格式：定长`FIXED`、动态`DYNAMIC`、压缩`COMPRESSED`
    
`InnoDB`存储引擎
- 设计遵循`ACID`模型`Atomicity`原子性、`Consistency`一致性、`Isolation`隔离性、`Durability`持久性，支持事务，具有从服务崩溃中恢复的能力，能够最大限度保护用户的数据
- 支持行级锁，可以提升多用户并发时的读写性能
- 支持外键，保证数据的一致性和完整性
- `InnoDB`拥有自己独立的缓冲池，常用的数据和索引都在缓存中
    

**记录`SQL`操作**

**添加记录**

    #一条记录用VALUE，多条记录用VALUES
    INSERT [INTO] table_name[(col_name1, col_name2...)] VALUE|VALUES(value1, value2...);
    
    #不列出字段名称[需要按照建表时的字段顺序给每一个字段赋值]
    INSERT [INTO] table_name VALUE(value1, value2...);
    
    #一次添加多条记录
    INSERT [INTO] table_name[(col_name1, col_name2...)] VALUES(value1, value2...), (value1, value2...),...;
    
    #INSERT...SET语句
    INSERT [INTO] table_name SET 字段名称=值,...;
    
    #INSERT...SELECT语句
    INSERT [INTO] table_name SELECT 字段名称,... FROM table_name [WHERE条件语句];
    

**修改记录**

    UPDATE table_name SET 字段名称1=值1, 字段名称2=值2,... [WHERE条件语句];

**删除记录**

    DELETE FROM table_name [WHERE条件语句];

**查询记录**

    # DESC：指定列按降序排列  ASC：指定列按升序排列
    # GROUP BY：分组，把值相同放到一个组里，最终查询出的结果只会显示组中一条记录，分组配合GROUP_CONCAT()查看组中某个字段的详细信息
    # ORDER BY：设置记录按照某字段的值进行排序，默认ASC升序
    # LIMIT：限制结果集的显示条数，可以用来实现分页
    		LIMIT 数字：显示结果集的前几条记录
    		LIMIT offset, row_count：从offset开始[offset从0开始]，显示几条记录
    SELECT 字段1, 字段2,... FROM table_name [WHERE条件语句] [GROUP BY(col_name) Having 二次筛选] [ORDER BY(col_name) DESC|ASC] [LIMIT 限制结果集的显示条数];
    
    #查询所有记录的所有字段
    SELECT * FROM table_name;
    
    #查询指定字段的信息
    SELECT 字段名称1, 字段名称2,... FROM table_name [WHERE条件语句];
    
    #查询某数据库下某表的记录[这样可以不用打开该数据库就能操作该表]
    SELECT 字段名称1, 字段名称2,... FROM db_name.table_name [WHERE条件语句];
    
    #给字段取别名[别名名称可以使用中文]
    SELECT 字段名称 [AS] 别名名称,... FROM table_name [WHERE条件语句];
    
    #给表取别名[单张表没有太大作用，多张表才体现]
    SELECT 字段名称1, 字段名称2,... FROM table_name [AS] 别名 [WHERE条件语句];
    
    #表名.字段名称[单张表没有太大作用，多张表才体现]
    SELECT table_name.字段名称,... FROM table_name [WHERE条件语句]
    
    #WHERE条件[筛选符合条件的记录]
    比较运算符：> < >= <= != <> <=>
    逻辑运算符：AND(逻辑与) OR(逻辑或)
    IS [NOT] NULL：检测值是否为NULL或者NOT NULL
    指定范围：[NOT] BETWEEN...AND
    指定集合：[NOT] IN(值1, 值2,..)
    匹配字符：[NOT] LIKE
    		%：任意长度的字符串
    		_：任意一个字符
    		
    #模糊查询
    在执行数据库查询时，分为完整查询和模糊查询。
    格式：SELECT 字段1, 字段2,.. FROM table_name WHERE 某字段 LIKE 条件;
    
    模糊查询包涵两种通配符：
    %：表示0个或多个字符，可以匹配任意类型或任意长度的字符。
    LIKE '%王'：匹配的是字段结尾为'王'的所有记录；
    LIKE '王%'：匹配的是字段开头为'王'的所有记录；
    LIKE '%王%'：匹配的是字段包含'王'的所有记录；
    
    _：表示任何单个字符，匹配单个任意字符，它常用来限制表达式的字符长度。
    LIKE '_王'：匹配的是字段长度为2，并且结尾为'王'的所有记录；
    LIKE '王_'：匹配的是字段长度为2，并且开头为'王'的所有记录；
    LIKE '_王_'：匹配的是字段长度为3，并且中间为'王'的所有记录；
    
    #常用聚合函数
    COUNT()：统计记录总数
    SUM()：求和
    MAX()：求最大值
    MIN()：求最小值
    AVG()：求平均值
    
    #产生随机数
    SELECT RAND();
    
    #实现随机记录[出现的记录排序是随机的]
    SELECT * FROM table_name ORDER BY RAND();
    
    
    #测试完整SELECT语句的形式
    MariaDB [test004]> SELECT GROUP_CONCAT(name) AS '姓名', COUNT(*) AS '人数', SUM(age) AS '总和', MAX(age) AS '最大', MIN(age) AS '最小', AVG(age) AS '平均' FROM user WHERE id >=1 GROUP BY address ORDER BY '总和';
    

**多表查询**

    1. 笛卡尔积形式
    笛卡尔积是多表连接组成一个新表的情况，所有的连接方式都会先生成临时笛卡尔积表，笛卡尔积是关系代数里的一个概念，表示两个表中的每一行数据任意组合，新表的记录数为多张表的记录条数的乘积，实际应用中一般不满足需求，只有在两个表连接时加上限制条件，才有实际的意义。
    
    test1				   test2
    +------+--------+		+------+--------+
    | id   | name   |		| id   | name   |
    +------+--------+		+------+--------+
    |    1 | 小红   |		   |    1 | 张三   |
    |    2 | 小明   |		   |    2 | 李四   |
    +------+--------+		+------+--------+
    
    MariaDB [test005]> select a.*, b.* from test1 a, test2 b;
    +------+--------+------+--------+
    | id   | name   | id   | name   |
    +------+--------+------+--------+
    |    1 | 张三   |    1 | 小红   |
    |    2 | 李四   |    1 | 小红   |
    |    1 | 张三   |    2 | 小明   |
    |    2 | 李四   |    2 | 小明   |
    +------+--------+------+--------+
    
    
    2. 内连接形式（常用）
    利用内连接可获取两表的公共部分的记录
    SELECT 字段名称,... FROM  table_name1 INNER JOIN table_name2 ON 连接条件
    
    3. 外连接形式
    左外连接：以左表为主，先显示左表中的全部记录，再去右表中查询满足复合条件的记录，不符合的以NULL代替
    SELECT 字段名称,... FROM table_name1 LEFT [OUTER] JOIN table_name2 ON 连接条件
    
    右外连接：以右表为主，先显示右表中的全部记录，再去左表中查询满足复合条件的记录，不符合的以NULL代替
    SELECT 字段名称,... FROM table_name1 RIGHT [OUTER] JOIN table_name2 ON 连接条件
    
    
**图形化工具管理数据库**

    B/S结构
    phpMyAdmin
    
    C/S结构
    Sequel Pro
    Navicat for MySQL
    MySQL workbench










