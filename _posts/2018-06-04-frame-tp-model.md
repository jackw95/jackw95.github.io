---
layout: post
title:  "Model篇"
date:   2018-06-04
categories: ThinkPHP
tags: thinkphp
excerpt: 模型篇
---

* content
{:toc}

#### `ThinkPHP`

**数据库操作**

**数据库连接**

    #在config/database.php设置数据库连接参数或者利用Db::connect()方法设置数据库连接
    
    /*
     * public static function connect($config = [], $name = false)
     * 数据库初始化，并取得数据库类实例
     * $config：数据库配置信息数组，可以在该方法里面进行配置
     */
    #
    var_dump(Db::connect());

**数据库查找**

`query`：直接操作`sql`语句

    /*
     * mixed query(string $sql, array $bind = [], boolean $master = false, bool $pdo = false)
     * 描述：SQL查询语句，然后array类型
     * $sql：SQL语句字符串
     * $bind：SQL语句中绑定的字符串
     */
    $res = Db::query('select * from book where id=?', [1001]);	

常用查询语句

    # select 返回所有记录，返回的结果是一个二维数组
    # 如果结果不存在，返回一个空数组'[]'
    $res = Db::table('book') ->where([
        'id'    => '1001'
    ])->select();
    
    $res = db('book') ->where([
        'id'    => '1001'
    ])->select();   #功能同上
    
    # find 返回一条记录，返回的结果是一个一维数组
    # 如果结果不存在，返回null
    $res = Db::table('book') ->where([
        'id'    => '1002'
    ])->find();
    
    $res = db('book') ->where([
        'id'    => '1001'
    ])->find();     #功能同上
    
    # value 返回一条记录，并且是这条记录的某个字段值
    # 如果结果不存在，返回null
    $res = Db::table('book') ->where([
        'id' => '1001'
    ])->value('name');
    
    $res = db('book') ->where([
        'id'    => '1001'
    ])->value('name');     #功能同上
    
    # column 返回一个一纬数组，数组中的value值就是我们要获取列的值
    # 如果结果不存在，返回空数组'[]'
    $res = Db::table('book') -> where([
        'id' => '1001'
    ]) -> column('name');
    
    $res = db('book') ->where([
        'id'    => '1001'
    ])->column('name');     #功能同上

数据库添加
`execute`：直接操作`sql`语句

    /*
     * integer execute(string $sql, array $bind = [], boolean $fetch = false, boolean $getLastInsID = false, string $sequence = null)
     * 描述：SQL更新语句
     * $sql：SQL语句字符串
     * $bind：SQL语句中绑定的字符串
     */
    $res = Db::execute('select * from book where id=?', [1002]);

常用插入语句

    public function insert()
    {
        //指定数据库表，获取表资源
        $db = Db::name('book');
    
        # $db ->insert()：插入单条记录，返回是影响记录的行数
        # $db ->insertGetId()：插入单条记录，返回的是插入记录的id
        # $db ->insertAll()：批量插入
    
        //inset 返回值是影响记录的行数，插入数
        $res = $db ->insert([
            'id'        => '1005',
            'name'      => '书籍5',
            'type_id'   => '1',
            'author'    => '赵六',
            'press'     => '牛津大学出版社'
        ]);
        
        dump($res);
    }

数据库更新

    public function update()
    {
        //指定数据库表
        $db = Db::name('book');
    
        # $db->update()
        # 更新记录某一个或几个字段，返回值为影响记录的行数
        $res = $db ->where([
            'id' => 1001
        ])->update([
            'author' => '比克'
        ]);
    
        # $db->setField()
        # 更新记录下某一个字段的值，返回值为影响记录的行数
        $res = $db ->where([
            'id' => 1001
        ])->setField('name', '书籍111');
    
        # $db->setInc()
        # 更新记录下某一个字段按固定步长增长，返回值为影响记录的行数
        $res = $db ->where([
            'id' => 1001
        ]) ->setInc('type_id', '2');
    
        # $db->setDec()
        # 更新记录下某一个字段按固定步长减小，返回值为影响记录的行数
        $res = $db ->where([
            'id' => 1001
        ]) ->setDec('type_id', '2');
    
        dump($res);
    }

数据库删除

    public function delete()
    {
        //指定数据库表
        $db = Db::name('book');
    
        #返回值为影响记录的行数
        $res = $db->where([
            'id' => 1001
        ])->delete();
    
        #如果where条件中是主键，则可以写为：
        $res = $db->delete('1002');
    
        dump($res);
    }

链式操作

    $res3 = Db::table('book')
            -> where('id', '>', '1004') 	#查询条件where($field, $op, $condition)
            -> field('name, press') 		#过滤条件field
            -> order('id DESC')     		#排序方式order,DESC降序，ASC升序
           # -> limit(3, 5)                  #记录条数限制limit
           # -> page(2,5)                    #分页功能page
            -> group('press')       		#分组group
            -> select();



**模型**

获取`model`对象

    public function requireModel()
    {
        #方式1：使用助手函数获取model实例对象
        $book = model('Book');
        $book1 = $book::get('1001');
    
        #方式2：使用Loader获取model实例对象
        $book = Loader::model('Book');
        $book2 = $book::get('1001');
    
        #方式3：使用new方法获取实例对象
        $book = new Book();
        $book3 = $book::get('1001');
    
        #方式4：静态方法直接获取实例对象（推荐使用）
        $book4 = Book::get(1001);
    
        dump($book1->toArray());
        dump($book2->toArray());
        dump($book3->toArray());
        dump($book4->toArray());
    }

模型查询数据

    public function getBook($bookId)
    {
        #get进行查找单条记录
        $book = Book::get($bookId);             #方法1
        $book = Book::get(function ($query){    #方法2
            $query->where('id', '>', 1001)
                ->field('name');
        });
        $name = $book->name;        #调用模型的属性
        $res = $book->toArray();    #将模型转换为数组
    
        #get获取批量记录
        $books = Book::all();
        $book = Book::all(function ($query){    #方法2
            $query->where('id', '>', 1001)
                ->field('name');
        });
        foreach ($books as $value)
        {
            #遍历循环打印
            #dump($value->toArray());
        }
    
        #和Db相似的链式方法：find()方法查找单条记录
        $res = Book::where('id', '=', '1001')
                ->field('name, author')
                ->find();
        #dump($res->toArray());
    
        #select()方法查找多条记录
        $res = Book::where('id', '>', '1001')
            ->field('name, author')
            ->select();
        foreach ($res as $value)
        {
            #遍历循环打印
            #dump($value->toArray());
        }
    
        #value()：获取单条记录某个字段的值
        $res = Book::value('press');
    
        #column()：所有多条记录某个字段的值
        $res = Book::column('press', 'press');
        dump($res);
    }

模型添加数据

    public function insertBook($bookId)
    {
        #方式1：Book::create插入单条数据
        $book = Book::create([
            'id'            => $bookId,
            'name'          => '书籍21',
            'type_id'       => 1,
            'author'        => "作者{$bookId}",
            'press'         => '清华大学出版社'
        ]);
    
        #方式2：save()插入单条数据
        $book = new Book();
        $book->id = 1000 + (integer)($bookId);
        $book->name = "书籍{$bookId}";
        $book->type_id = 1;
        $book->author = "作者{$bookId}";
        $book->press = '清华大学出版社';
        $book->save();
    
        $book1 = new Book();    #插入快捷方式
    	$book1->save([
    		'id'            => 1000 + (integer)($bookId),
    		'name'          => "书籍{$bookId}",
    		'type_id'       => 1,
    		'author'        => "作者{$bookId}",
    		'press'         => '清华大学出版社'
    	]);
    
    	#方式3：saveAll()插入批量数据
        $res = $book1 ->saveAll([
            [
                'name'          => "书籍{$bookId}",
            ],
            [
                'name'          => "书籍{$bookId}",
            ]
        ]);
    
        dump($res);
    }

模型更新数据

    public function updateBook()
    {
        //更新数据
        $res = Book::update([
            'author' => '作者11'
        ], function ($query){
            $query->where('id', '=', '1001');
        });
    
    
        #更新数据
        $res = Book::where('id', '=', '1002')
            ->update([
                'author' => '作者22'
            ]);
    
        #通过save()来更新已经有的model
        $book = Book::get(1001);
        $book ->author = '作者1';
        $book ->save();
    
        dump($book->toArray());
    }

模型删除数据

    public function deleteBook()
    {
        #Book::destroy()
    
        #如果当前表存在主键，直接传值
        #$res = Book::destroy(1001);
    
        #如果当前表不存在主键，则可以根据$query函数进行条件删除
        #$res = Book::destroy(function ($query){
        #    $query->where('id', '=', '1002');
        #});
    
        #通过实例进行删除
        #$book = Book::get(1003);
        #$res = $book ->delete();
    
        #通过where条件进行删除
        $res = Book::where('id', '>', 1000)
                ->delete();
    
        dump($res);
        
    }

模型聚合操作

    class Book extends Model
    {
        #属性和数据库表字段映射
        protected $createTime = 'create_time';
        protected $updateTime = 'update_time';
    
        #获取器：读取数据库中值的时候，在值的基础上进行修改
        public function getSexAttr($var)
        {
            switch ($var) {
                case 0:
                    return '男';
                    break;
                case 1:
                    return '女';
                    break;
                default:
                    return '未知';
                    break;
            }
        }
    
        #修改器：对写入数据库中值进行修改
        public function setPasswordAttr($var)
        {
            return md5($var);
        }
    
    
        #自动完成功能
        protected $auto = [     #数据插入或更新的时候，对字段进行更新
    
        ];
    
        protected $insert = [   #插入时候，对字段进行更新
            'create_time'
        ];
    
        protected $update = [   #更新时候，对字段进行更新
            'modify_time'
        ];
    
        #绑定数据库中create_time字段
        public function setCreateTimeAttr($var)
        {
            return time();
        }
    
        #绑定数据库中modify_time字段
        public function setModifyTimeAttr($var)
        {
            return time();
        }
    }

了解：`SoftDelete`（软删除）


