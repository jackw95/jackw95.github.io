---
layout: post
title:  "Trait"
date:   2018-04-16
categories: PHP基础
tags: php
excerpt: 自PHP 5.4.0起，实现了一种代码复用的方法
---

* content
{:toc}

**自 `PHP 5.4.0` 起，`PHP` 实现了一种代码复用的方法，称为 `Trait`。**

`Trait` 是为类似 `PHP` 的单继承语言而准备的一种代码复用机制。`Trait` 为了减少单继承语言的限制，使开发人员能够自由地在不同层次结构内独立的类中复用 `method`。 

- _`trait`看上去更像是为了代码的复用而写的一个小插件，它类似于`include` 可以用`use`放在类中间，让`trait`里面定义的方法作为`class`的一部分 本身不能直接实例化，`Trai`t的作用域在引用该`Trai`t类的内部是都可见的(`public`、`private` 等等都可以) 可以理解为`use`关键字将`Trait`的实现代码`Copy`了一份到引用该`Trait`的类中 。_

```

<?php trait ezcReflectionReturnInfo {
    function getReturnType() { /*1*/ }
    function getReturnDescription() { /*2*/ }
}

class ezcReflectionMethod extends ReflectionMethod {
    use ezcReflectionReturnInfo;
    /* ... */ }

class ezcReflectionFunction extends ReflectionFunction {
    use ezcReflectionReturnInfo;
    /* ... */ } ?>

```

#### 优先级

从基类继承的成员会被` trait` 插入的成员所覆盖。优先顺序是来自当前类的成员覆盖了 `trait` 的方法，而 `trait` 则覆盖了被继承的方法。

```

<?php class Base {
    public function sayHello() {
        echo 'Hello ';
    }
}

trait SayWorld {
    public function sayHello() {
        parent::sayHello();
        echo 'World!';
    }
}

class MyHelloWorld extends Base {
    use SayWorld;
} $o = new MyHelloWorld(); $o->sayHello();    #输出：Hello, World! ?> 

```

```

<?php trait HelloWorld {
    public function sayHello() {
        echo 'Hello World!';
    }
}

class TheWorldIsNotEnough {
    use HelloWorld;
    public function sayHello() {
        echo 'Hello Universe!';
    }
} $o = new TheWorldIsNotEnough(); $o->sayHello();    #输出：Hello Universe!  ?>

``` 
#### 多个 trait[ ](https://php.net/manual/zh/language.oop5.traits.php#language.oop5.traits.multiple) 

通过逗号分隔，在 `use` 声明列出多个` trait`，可以都插入到一个类中。

```
<?php trait Hello {
    public function sayHello() {
        echo 'Hello ';
    }
}

trait World {
    public function sayWorld() {
        echo 'World';
    }
}

class MyHelloWorld {
    use Hello, World;
    public function sayExclamationMark() {
        echo '!';
    }
} $o = new MyHelloWorld(); $o->sayHello(); $o->sayWorld(); $o->sayExclamationMark(); ?>
```

如果两个 `trait` 都插入了一个同名的方法，如果没有明确解决冲突将会产生一个致命错误。

引用地址：https://www.php.net/traits







