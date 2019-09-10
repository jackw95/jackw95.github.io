---
layout: post
title:  "文件函数库"
date:   2017-05-30
categories: PHP基础
tags: php
excerpt: PHP基础
---

* content
{:toc}

#### 文件函数库
**文件、目录函数库为`PHP`核心函数库，可以通过其提供的`API`完成对于文件及目录的常用操作。**

**文件信息相关的`API`**

    /*
     * 文件信息相关API
     * filetype(), filesize(), filectime(),filemtime(), fileatime()
     */
    
    $dirname = "./";
    $filename = "./11.txt";
    
    // string filetype(string filename)：返回文件的类型
    echo '文件类型为：', filetype($dirname), "\n";        //dir
    echo '文件类型为：', filetype($filename), "\n";       //file
    
    //int filesize(string filename)：返回文件大小的字节数
    echo '文件大小：', filesize($filename), "\n";
    
    //int filectime(string filename)：返回文件的创建时间的时间戳
    echo '文件的创建时间：', date('Y-m-d H:i:s', filectime($filename)), "\n";
    
    //int filemtime(string filename)：返回文件的最后修改时间的时间戳
    echo '文件的修改时间：', date('Y-m-d H:i:s', filemtime($filename)), "\n";
    
    //int fileatime(string filename)：返回文件的最后访问时间的时间戳
    echo '文件的最后访问时间：', date('Y-m-d H:i:s', fileatime($filename)), "\n";
    
    //检测文件是否可读、可写、可执行：is_readable(), is_writeable(), is_executabel()
    //var_dump(is_readable($filename));       //bool(true)
    //var_dump(is_writable($filename));       //bool(true)
    //var_dump(is_executable($filename));     //bool(false)
    //var_dump(is_file($filename));           //bool(true)
    var_dump(
        is_readable($filename),
        is_writable($filename),
        is_executable($filename),
        is_file($filename)
    );  //功能同上四句

**文件路径相关`API`**

    /*
     * mixed pathinfo(string $path, [, int $options = PATHINFO_DIRNAME | PATHINFO_BASENAME | PATHINFO_EXTENSION | PATHINFO_FILENAME ])
     * 描述：返回文件路径的信息。后面接常量表示具体的值
     *
     * PATHINFO_DIRNAME：文件夹名
     * PATHINFO_BASENAME：文件全称
     * PATHINFO_EXTENSION：文件扩展名
     * PATHINFO_FILENAME：文件名称
     */
    print_r(pathinfo($filename));  //Array([dirname] => .  [basename] => 11.txt [extension] => txt [filename] => 11)
    echo pathinfo($filename, PATHINFO_EXTENSION), "\n";  //取出扩展名
    
    $filename = __FILE__;
    echo pathinfo($filename, PATHINFO_DIRNAME), "\n";  //路径部分
    echo pathinfo($filename, PATHINFO_EXTENSION), "\n";  //文件扩展名部分
    
    //string basename(string $path[, string $suffix])
    //描述：给出一个包含有指向一个文件的全路径的字符串，返回基本的文件名，如果文件名是以suffix🉑️🉑️结束的，那这一部分也会被去掉
    echo basename($filename), "\n";  //文件路径下的文件全程
    
    //string dirname(string $path)：给出一个包含有指向文件的全路径的字符串，返回去掉文件名后的目录名
    echo dirname($filename), "\n";     //文件路径
    
    //bool file_exists(string $filename)：检查文件或目录是否存在
    var_dump(file_exists($filename));

**文件相关的`API`**

    //文件创建、删除、剪切、重命名、拷贝
    
    /*
     * bool touch(string $filename[, int $time=time()[, int $atime]])
     * 描述：如果文件存在，则尝试将由filename给出的文件的访问和修改时间设定为给出的time，
     *      如果文件不存在，则会被创建
     * 参数：
     * filename：要设定的文件名
     * time：要设定的时间，没有提供则会使用当前系统的时间
     * atime：如果给出了这个参数，则给定文件的访问时间会被设置为atime，否则设置为time
     *
     */
    $filename = './22.txt';
    var_dump(touch($filename));
    
    /*
     * bool unlink(string $filename[, resource $context])
     * 描述：删除指定路径下的文件
     *
     */
    if (file_exists($filename)){  //如果文件存在则删除
    //    var_dump(unlink($filename));
    }
    
    /*
     * bool rename(string $oldname, string $newname[, resource $context])
     * 描述：重命名一个文件或者目录
     *
     */
    if (file_exists($filename)){  //如果文件存在则重命名
        $newName = './44.txt';
        var_dump(rename($filename, $newName));
    }
    
    $oldname = '../practice';
    if (file_exists($oldname)){  //如果目录存在则重命名
        $newname = '../practices';
        var_dump(rename($oldname, $newname));
    }
    
    //将11.txt剪切到aaa目录下
    $filename = './11.txt';
    $newname = './aaa/11.txt';
    if (file_exists($newname)){
        //只需要将文件重命名就能实现其路径的切换
        var_dump(rename($newname, $filename));
    }
    
    /*
     * bool copy(string $source, string $dest)
     * 描述：将文件重source拷贝到dest，如果用移动，请用rename
     *
     * 注意：只能移动具体文件，不能移动目录
     */
    $filename = './11.txt';
    $desname = './aaa/1.txt';
    if (file_exists($filename)){
        var_dump(copy($filename, $desname));
    }
    
    
    $imageName = 'http://pic4.nipic.com/20091217/3885730_124701000519_2.jpg';
    $newName = './aaa/image1.jpg';
    //拷贝远程文件需要开启php.ini文件中的allow_url_fopen=On选项
    var_dump(copy($imageName, $newName));  //将http网络上的资源拷贝过来
    
    //var_dump(rename($imageName, $newName));  //http wrapper does not support renaming 不能移动http网络上的资源
    

**文件内容相关`API`**

    //内容相关操作
    /*
     * 打开文件
     * resource fopen(string $filename, string $mode)
     * 描述：打开文件或者url
     * $filename：指定的文件名
     * $mode：指定了所要求到该流的访问类型：
     * 'r'：只读方式打开，将文件指针指向文件头
     * 'r+'：读写方式打开，将文件指针指向文件头
     * 'w'：写入方式打开，将文件指针指向文件头并将文件大小截为零
     * 'w+'：读取方式打开，将文件指针指向文件头并将文件大小截为零
     * 'a'：写入方式打开，将文件指针指向文件末尾
     * 'a+'：读写方式打开，将文件指针指向文件末尾
     * 'x'：创建并以写入方式打开
     * 'x+'：创建并以读写方式打开
     *
     *
     * 读取、写入文件
     * string fread(resource $handle, int $length)
     * 描述：读取文件，返回一个字符串。fread()从文件指针handle读取最多length个字节。
     * 该函数在遇到以下几种情况停止读取文件：
     * 读取了length个字节;
     * 到达了文件末尾EOF;
     *
     * int ftell(resource $handle)
     * 描述：返回文件指针读/写的位置
     *
     * int fseek(resource $handle, int $offset)
     * 描述：在文件指针中定位
     *
     * bool rewind(resource $handle)
     * 描述：倒回文件指针的位置，将handle的文件位置指针设为文件流的开头
     *
     * bool ftruncate(resource $handle, int $size)
     * 描述：将文件截断到给定的长度
     *
     * 
     * int fwrite(resource $handle, string $string[, int $length]) 注：fputs()是fwrite的别称
     * 描述：写入文件。把string写入文件指针handle处
     * 如果指定了length，当写入了length个字节或者写完了string以后，写入就会停止。
     * 注意：fwrite向文件写入内容，如果之前有内容，会产生覆盖
     *
     *
     * 关闭文件
     * bool fclose(resource $handle)
     * 描述：关闭一个已经打开的文件指针
     *
     */
     $filename = '../aaa/1.txt';
    
    //操作$handle对象的时候，要时刻注意文件指针的位置
    
    //将文件内容设置为'this is a test'
    $handle = fopen($filename, 'w');
    fwrite($handle, 'this is a test');
    fclose($handle);
    
    /*
     * 'r'：只读方式打开，将文件指针指向文件头
     * 'r+'：读写方式打开，将文件指针指向文件头
     */
    $handle1 = fopen($filename, 'r');
    echo fread($handle1, filesize($filename)), "\n";
    fclose($handle1);
    
    //注：fwrite()向文件写入内容，如果之前的位置有内容，会产生覆盖
    $handle2 = fopen($filename, 'r+');
    if (fwrite($handle2, 'aaa')){
    //    fseek($handle2, 0);  //将文件指针指向第一个位置
        rewind($handle2);  //功能同上，将文件指针指向第一个位置
        echo fread($handle2, filesize($filename)), "\n";
    }
    fclose($handle2);
    
    
    /*
     * 'w'：写入方式打开，将文件指针指向文件头并将文件大小截为零。如果文件不存在则尝试创建之
     * 'w+'：读写方式打开，将文件指针指向文件头并将文件大小截为零。如果文件不存在则尝试创建之
     */
    $handle3 = fopen($filename, 'w');
    fwrite($handle3, 'aaa123');
    fclose($handle3);
    
    $handle4 = fopen($filename, 'w+');
    if (fwrite($handle4, 'abc')){
        fseek($handle4, 0);
        echo fread($handle4, filesize($filename)), "\n";
    }
    fclose($handle4);
    
    /*
     * 'a'：写入方式打开，将文件指针指向文件末尾。如果文件存在则尝试创建之
     * 'a+'：读写方式打开，将文件指针指向文件末尾。如果文件存在则尝试创建之
     */
    //PHP_EOL：相当于'\n'换行符号
    $handle5 = fopen($filename, 'a');
    fwrite($handle5, 'handle5');
    fclose($handle5);
    
    $handle6 = fopen($filename, 'a+');
    if (fwrite($handle6, 'handle6')){
        fseek($handle6, 0);
        echo fread($handle6, filesize($filename)), "\n";  //abchandleahand 疑问：为什么少了'le6'
    
        ftruncate($handle6, 5);  //将文件截取到给定的长度
    
        rewind($handle6);
        echo fread($handle6, filesize($filename)), "\n";
    }
    fclose($handle6);
    
    
    
    
    /*
     * string fgetc(resource $handle)
     * 描述：从文件句柄中获取一个字符，如果碰到EOF则返回false
     *
     * string fgets(resource $handle[, int $length])
     * 描述：从文件指针中读取一行
     * length：限制取回该长度的数据
     *
     * string fgetss(resource $handle[, int $length[, string $allow_tags]])
     * 描述：从文件指针中读取一行并过滤掉html标记。和fgets()相同，只除了fgetss()尝试从读取的文本中去掉任何html和php标记
     * length：限制取回该长度的数据
     *
     * bool feof(resource $handle)：测试文件指针是否到了文件结束的位置
     *
     * string strip_tags(string $str[, string $allow_tags])
     * 描述：从字符串中取出html和php标记
     *
     * 注意：
     * fgetcsv()
     * fputcsv()
     *
     */
    
    $filename = '../aaa/1.txt';
    
    //写入一段文件
    $handle1 = fopen($filename, 'w');
    $txt = <<<EOF
    <h1>一级标题</h1>
    <h2>二级标题</h2>
    <h3>三级标题</h3>
    EOF;
    fwrite($handle1, $txt);
    fclose($handle1);
    
    
    $handle2 = fopen($filename,'r+');
    echo fread($handle2, filesize($filename)), "\n";
    
    rewind($handle2);
    echo '第一个字符是：', fgetc($handle2), "\n";  //第一个字符是：<
    
    
    rewind($handle2);
    echo '第一行字符串是：', fgets($handle2), "\n";  //第一行字符串是：<h1>一级标题</h1>
    
    rewind($handle2);
    while (!feof($handle2)){  //利用feof()函数判断是否为文件结尾，遍历输出每一行
        echo fgets($handle2);
    }
    echo "\n";
    
    rewind($handle2);
    echo fgetss($handle2), "\n";  //一级标题
    
    rewind($handle2);
    echo strip_tags(fgets($handle2)), "\n";  //功能同上
    fclose($handle2);
    

**简化的读取、写入文件**

    /*
     * 简化的读取、写入文件
     *
     * string file_get_contents(string $filename[, bool $use_include_path=false[, ...]])
     * 描述：将整个文件读入一个字符串
     *
     * int file_put_contents(string $filename, mixed $data[, int....])
     * 描述：将一个字符串写入文件。会将之前的内容清空
     * data：要写入的数据，类型可以是string, array或者是stream资源，data可以是数组，但不能是多纬数组
     *       一般只是写入string类型
     * 注意：如果$filename下的文件不存在，会自动创建文件
     *
     *
     * 序列化和反序列化：
     *
     * string serialize(mixed $value)
     * 描述：产生一个可存储的值的表示，称为序列化
     *
     * mixed unserialize(string $str)
     * 描述：从已存储的表示中创建php的值，称为反序列化
     *
     *
     * php变量和json的相互转化：
     *
     * string json_encode(mixed $value...)
     * 描述：对变量进行json编码，返回json字符串
     *
     * mixed json_decode(string $json...)
     * 描述：对json格式的字符串进行解码，转换成php变量
     *
     *
     */
    echo '简化函数：', "\n";
    $filename = '../aaa/1.txt';
    echo file_get_contents($filename), "\n";
    
    $string = '你好吗，我是昭哥';
    file_put_contents($filename, $string);
    echo file_get_contents($filename), "\n";
    
    $arr = [
        'id' => 1001,
        'name' => '王昭',
        'sex' => '男',
        'phone' => '1829210000',
    ];
    $string = serialize($arr);
    echo $string, "\n";  //a:5:{i:0;i:1;i:1;i:2;i:2;i:3;i:3;i:4;i:4;i:5;}  ->将$arr序列化为字符串
    print_r(unserialize($string));  //Array([0] => 1 [1] => 2 [2] => 3 [3] => 4 [4] => 5) ->将序列化后的字符串反序列化为数组
    
    $json = json_encode($arr);
    echo $json, "\n";
    
    print_r(json_decode($json));


