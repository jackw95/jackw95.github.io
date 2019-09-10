---
layout: post
title:  "Javascript下"
date:   2018-06-04
categories: Web前端
tags: web
excerpt: 基于客户端浏览器、基于面向对象、事件驱动式的网页脚本语言
---

* content
{:toc}

#### 关于函数
**函数是可重复执行的包含特定功能的代码段。**
    
`js`中的**命名函数**和**匿名函数**

    <button id="btn1" onclick="func()">点击我吧</button>
    <button id="btn2">点击它吧</button>    
    
    <script>
        //命名函数
        function func(){
            //代码段
            alert('点击我吧');
        }
        
        //匿名函数
        var btn2 = document.getElementById('btn2');
        btn2.onclick = function(){
            //代码段
            alert('点击它吧');
        }
    </script>
    
####关于`DOM`
`DOM`：`Document Object Model`，称为文档对象模型，在网页加载时，可以将结构化文档在内存中转换为对象结构树。简单的说，`DOM`并不是一种技术，而是一种访问结构化文档的一种思想。借用`DOM`模型，我们可以对`DOM`树进行修改、删除、新增等操作，让结构化文档动态化。
`DOM`模型中的节点--文档可以说是由节点构成的集合。在`DOM`模型中有以下3种节点：
- 元素节点：各种标签就是这些元素节点的名称，如`<p>`、`<ul>`等
- 属性节点：一般用来修饰元素节点就称为属性节点
- 文本节点：文本节点总是被包含在元素节点的内部

注：为了动态地修改`html`元素，须先访问`html`元素。

**查找`HTML`元素**

    document.getElementById()            //id   
    document.getElementsByClassName()    //class
    document.getElementsByName()         //name
    document.getElementsByTagName()      //tagName
    
**对元素节点的操作：**

    //创建节点
    document.createElement(tag);    //tag必须是合法的html元素
    
    //复制节点
    document.cloneNode(boolean deep);    //deep为true，复制所有后带节点，为false，只复制当前节点
    
    //添加节点
    node.appendChild(newNode)
    node.insertBefore(newNode, refNode)
    
    //修改
    node.replaceChild(newNode, oldNode)
    
    //删除
    node.removeChild(oldNode)

**对属性节点的操作：**

```
//添加
node.setAttribute('属性名', '值');

//删除
node.removeAttribute('属性名');

//修改
node.setAttribute('属性名', '值');

//查询
node.getAttribute('属性名')

```
**对文本节点的操作：**

    //添加、删除、修改、查询
    node.innerHTML = '';

注：通过`DOM`还可以修改`HTML`标签节点的样式：
`document.getElementById(id).style.property = new style`





