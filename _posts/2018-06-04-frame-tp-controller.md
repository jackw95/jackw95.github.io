---
layout: post
title:  "Controller篇"
date:   2018-06-04
categories: ThinkPHP
tags: thinkphp
excerpt: 控制器篇
---

* content
{:toc}

#### `ThinkPHP`

_`ThinkPHP`是一个免费开源的、快速简单的、面向对象的、轻量级`PHP`开发框架。_

**为什么选择`ThinkPHP5`？**
- `ThinkPHP5`采用了全新的架构思想;
- 优化了核心是一个颠覆性的版本;
- 支持`composer`方式安装;
- 对`API`进行了大量的优化更符合了现代`web`开发的方式;

**`MVC`定义：**
`MVC`全名`Model-View-Controller`，是模型、视图、控制器的缩写，是一种软件设计典范，而不是一种设计模式。其特点：
- 耦合性低
- 重用行高
- 可维护性高
- 有利于软件的工程化

**开发环境：**
`PHP` >= 5.4.0
`Mysql`
`Apache/Nginx`

`Mysql`默认端口号`3306`，`Apache/Nginx`默认端口号`80`

**三种安装方法：**
- `github`上下载`think`, `framework`
- `composer`下载
- `thinkphp`官网下载



**`composer`简介**
`composer`是`php`的一个依赖管理工具
文档：http://docs.phpcomposer.com/
安装：

    curl -sS https://getcomposer.org/installer | php		#下载composer安装工具
    sudo mv composer.phar /usr/local/bin/composer			#将下载下来的composer.phar移动到系统的PATH目录，这样全局能够进行访问。

`composer`安装`TP5`
`composer create-project --prefer-dist topthink/think proj_name`

**`Apache`设置根目录**

`/Applications/XAMPP/etc/httpd.conf`文件为`Apache`的核心配置文件，打开后重新设置`DocumentRoot`的值，`DocumentRoot`为`web`的根目录，然后重启`Apache`服务器即可。

**`TP5`目录讲解**

    tp5
    |-application					#应用目录
    	|-index
    		|-controller	#控制器
    		|-view			#视图
    		|-model			#模型
    	|-command.php		#控制台的配置文件
    	|-common.php		#项目全局的公共文件
    	|-config.php		#应用的配置文件
    	|-database.php		#数据库配置文件
    	|-route.php			#路由文件
    	|-tag.php			#应用行为扩展文件
    |-extend						#扩展类库目录
    |-public						#网站对外访问目录
    	|-index.php			#应用入口文件，所有的请求都是通过index.php之后进行转发
    	|-robots.text		#定义哪些文件能被搜索引擎爬取，哪些不能
    	|-router.php		#框架快速启动的配置文件
    	|-static			#存放网站的静态资源，如css,html,image等
    |-runtime						#运行时目录，包含项目运行时的缓存文件、编译文件、日志等
    |-thinkphp						#框架核心目录
    	|-lang				#语言包目录
    	|-library			#框架核心类库目录
    	|-tpl				#系统模版文件
    	|-base.php			#框架基础文件，常用于定义一些常量
    	|-composer.json		#composer定义文件
    	|-console.php		#控制台入口文件
    	|-convention.php	#惯例配置文件
    	|-helper.php		#助手函数文件
    	|-phpunit.xml		#单元测试配置文件
    	|-README.md			#README文件
    	|-start.php			#框架引导文件
    |-vendor						#第三方类库目录
    |-bulid.php						#自动生成定义文件
    |-composer.json					#composer定义文件
    |-LICENSE.text					#授权说明文件
    |-README.md						#README文件
    |-think							#命令行工具入口

**开发规范：**
- 目录名使用小写+下划线的方式命名
- 类文件名采用大驼峰法，类文件中的类和类文件名一致，其他文件名均使用小写
- 方法名采用小驼峰法
- 属性名采用小驼峰法
- 以双下划线`__`开头的方法属于魔术方法
- 常量以大写字母和下划线命名
- 配置参数以小写字母和下划线命名
- 数据库表和字段采用小写`+`下划线的命名方式 不能以下划线开头
- 应用类库的命名空间统一为`app`（可以配置）



**`ThinkPHP5`模块设计**
`5.0`版本对模块的功能做了灵活设计，默认采用多模块的架构，并且支持单一模块设计，所有模块的命名空间均以`app`作为根命名空间（可配置更改，一般不进行更改）。
注意：`application`目录下创建的`common`文件夹，`common`会默认作为公共模块，里面的文件，不能通过url直接访问

设置命名空间：`namespace app\index\controller`;
设置别名：`use app\common\controller\Index as commonIndex`;

**`ThinkPHP5`配置**
- 惯例配置
    `ThinkPHP`框架下的默认配置，在`think/convention.php`文件中，一般不进行修改。

- 应用配置
    应用配置文件是应用初始化的时候首先加载的公共配置文件，默认位于`application/config.php`，作用域为整个应用项目。可以在入口文件`public/index.php`中定义`CONF_PATH`，然后新建文件夹，达到将应用配置放到该文件的目的，这样方便将配置进行统一管理。
    在`config`目录下创建`config.php`，添加应用配置或者对惯例配置进行修改（需要更改惯例配置时，一般不在原文件中直接更改，可以在创建的`config.php`中进行更改）
    在`config`目录下创建`database.php`，在里面配置数据库连接
    ```
    //定义配置文件目录
    define('CONF_PATH', __DIR__ . '/../application/config/');
    ```
- 扩展配置
    在上面应用配置`config`目录下添加名为`extra`的文件夹，然后添加配置文件，将会以数组形式作为元素添加到应用配置下。

- 场景配置
    在不同场景下设置不同的配置，可以利用设置数据库的连接参数
    `home.php`：家庭办公环境的配置项
    `office.php`：公司办公环境的配置项
- 模块配置
    模块配置文件是针对某个模块下的配置文件，一般位于`application/模块名/config.php`，可以在和`application`同级目录下创建文件路径`config/index/config.php`，然后在`public/index.php`中定义`CONF_PATH`为该路径，这种情况也分为应用配置`config/config.php`和模块配置`config/index/config.php`，但会忽略`application`路径下的配置。
- 动态配置
    在具体的控制器或者方法里面进行动态配置，动态配置只在当前的控制器或者当前的方法中有效。比如在`Index.php`下设置如下代码，就可以为`Index`控制器动态的添加或修改配置。
    ```
    public function __construct()
    {
        config('before', 'beforeAction');
        Config::set('before', 'beforeAction');  //功能同上，动态配置
    }
    ```
    

**`Config`类下的方法**
目录：`thinkphp/library/think/Config.php`
`range($range)`：设定配置参数的作用域
`parse($config, $type = '', $name = '', $range = '')`：解析配置文件或内容
`load($file, $name = '', $range = '')`：加载配置文件（PHP格式）
`has($name, $range = '')`：检测配置是否存在
`get($name = null, $range = '')`：获取配置参数 为空则获取所有配置
`set($name, $value = null, $range = '')`：设置配置参数 `name` 为数组则为批量设置
`reset($range = '')`：重置配置参数

**环境变量配置和使用**
- 入口文件
    单入口文件：应用程序的所有http请求都由某一个文件接受并由这个文件转发到功能代码中。ThinkPHP符合这种功能规范，所有的http请求都由public/index.php文件接收并转发，根据不同的参数，转发到不同的控制器调用不同的方法，最终实现不同的功能。

- 隐藏入口文件
    ```
    public/.htaccess里面：
    
    # 将请求转发到index.php之后
    RewriteRule ^(.*)$ index.php/$1 [QSA,PT,L]
    ```
- 入口文件绑定
    ```
    public/index.php中添加：
    
    define('BIND_MODULE', 'admin');		   #绑定模块为admin，只能访问admin模块下的所有文件
    define('BIND_MODULE', 'admin/Index');  #绑定的模块为admin下的Index控制器，只能访问Index控制器下的所有方法
    ```
    
    可以在`public`目录下添加文件`api.php`，然后在文件下定义应用目录、加载框架引导文件等..，然后进行模块绑定，这样可以实现通过访问`api.php`下的模块实现让用户只能访问具体模块`api`下的文件，这样一个项目中可以进行多种开发（`API`开发等）。
    
    应用配置中：
    `auto_bind_module`：自动绑定模块
    其值设置为`true`之后
    入口文件`api.php`会自动绑定为`api`模块
    但入口文件`index.php`不会自动绑定为`index`模块
    
**路由**
将请求地址`url`和具体控制器中的具体方法绑定，通过路由来转发使其对应。

在`conf/config.php`中添加（也可以不添加，系统默认开启路由）：
    'url_route_on'           => true

在`index/Index`控制器下有方法：

    public function info($id = '')
    {
        return "{$id}";
    }

然后在`config/route.php`中添加：

    return [
        //设置路由
        'info/:id' => 'index/Index/info'
    ];

这样就实现了通过访问`localhost/info/5`可以访问`localhost/index/Index/info/5`。

**请求对象`Request`**
`ThinkPHP`是一个单入口框架，所有的请求都通过`index.php`，可以通过`index.php`来接收所有的`http`请求，请求中的所有参数都可以通过`Request`对象来接收。

获取`Request`对象的三种方式：

    public function index()
    {
        //获取方式一：通过助手函数request()
        $request = request();
        
        //获取方式二：通过Request对象实例
        $request = Request::instance();
    }
    
    //获取方式三：通过注入对象的方式（常用）
    public function index(Request $request)
    {
        dump($request);
    }

`Request`中常用方法：

    #注意：Requset中所有的方法都在thinkphp/think/Request.php文件中，可查阅
    
    public function index(Request $request)
    {
        #url信息
        dump($request->domain());                  #域名
        dump($request->pathinfo());                #url的pathinfo信息（含URL后缀）
        dump($request->path());                    #url的pathinfo信息(不含URL后缀)
        dump($request->url());                     #url
        
        #请求方式 GET、POST
        dump($request->method());				  #请求方式
        dump($request->isGet());                   #是否为GET请求
        dump($request->isPost());                  #是否为POST请求
        dump($request->isAjax());                  #是否为AJAX请求
        
        #请求参数
        dump($request->get());                     #获取所有参数的数组
        dump($request->param());                   #获取所有参数的数组（包含get、post、pathinfo等）
        dump($request->get('name'));       		   #获取name参数的值
        dump($request->get('age'));         	   #获取age参数的值
        dump($request->param('name'));      	   #获取name参数的值
        dump($request->param('age'));      		   #获取age参数的值
        
        #获取模型 控制器 操作
        dump($request->module());                   #当前模块
        dump($request->controller());               #当前控制器
        dump($request->action());                   #当前方法
    }

`input`助手函数

    /*
     * function input($key = '', $default = null, $filter = ...)
     * $key：表示传入参数
     * $default：参数默认值
     * $filter：参数过滤函数
     * 获取输入数据 支持默认值和过滤
     * 
     * 其中$key支持'.'语法，支持如下：
     * ['get', 'post', 'put', 'patch', 'delete', 'route', 'param', 'request', 'session', 'cookie',   'server', 'env', 'path', 'file']
     *
     */
    public function index(Request $request)
    {
        $res_get = $request->get('name');
        $res_param_get = $request->param('name');
        $res_input_get = input('get.name');  		 #功能同上，获取get请求中参数name对应的数据
        $res_input_get1 = input('get.name', '张三');	#如果参数name对应的数据为null，设置默认值
        
        $res_post = $request->post('name');
        $res_param_get = $request->param('name');
        $res_input_post = input('post.name');  		  #功能同上，获取post请求中参数name对应的数据
    }
    
    

**响应对象`Response`**

    http对每个请求都有相应的响应。
    
    public function getUserInfo()
    {
        //动态配置返回数据类型
        //config('default_return_type', 'json');
        Config::set('default_return_type', 'json');  //功能同上
    
        $res = [
            'code'  => 200,
            'body'  => [
                'name'  =>  '张三',
                'age'   =>   22,
                'sex'   =>   '男'
            ],
            'msg'  => '请求成功'
        ];
        return $res;
    }












