---
layout: post
title:  "JQuery"
date:   2018-06-06
categories: Web前端
tags: web
excerpt: 快速、简洁的`JavaScript`框架
---

* content
{:toc}

###`jQuery`
快速、简洁的`JavaScript`框架，设计宗旨：**_write Less, Do More_**。
作用：简化原生`js`的语法，解决浏览器兼容性问题。

**引入`jQuery`**
可以直接引入在线地址，也可以在`jQuery`[官方网站][1]上下载，然后使用`src`属性引入：
    <script src="jquery-3.3.1.js"></script>
  [1]: https://jquery.com/

**基础语法：`$(selector).action()`**
- `$`：`jQuery`对象
- `selector`：选择器，用于定位`HTML`元素
- `action()`：方法，用于对元素进行操作

**文档就绪函数**
```
//HTML文档加载完成后，再开始执行该方法里面的函数
$(document).ready(function(){
    //代码段
})
```

####`jQuery`选择器
`jQuery`选择器相比原生`javascript`功能更加强大

**元素选择器**
- `$('#id')`：`id`选择器，类似`document.getElementById("#id")`
- `$('.class')`：`class`选择器，类似`document.getElementsByClassName('.class')`
- `$('tag')`：`tag`选择器，类似`document.getElementsByTagName('tag')`
- `$('tag.class')`：父子选择器

**属性选择器**
- `$("[attr]")`：选取所有带有`attr`属性的元素
- `$("[attr='value']")`选取所有带有`attr`属性并值为`value`的元素
- `$("[attr$='value']")`选取所有带有`attr`属性并以`value`结尾的元素

####`jQuery`事件
事件方法会触发匹配元素的事件，或将函数绑定到所有匹配元素的某个事件。

**常用事件：**
`ready()`：文档就绪事件，`HTML`加载完成后调用
`bind()`：为被选元素添加一个或多个事件处理程序，并规定事件发生时运行的函数
`focus()`：当元素获得焦点的时候调用
`blur()`：当元素失去焦点的时候调用
`change()`：当元素的值发生改变时调用（仅仅适用于`form`表单中的`text`、`field`、`select`、`textarea`）
`click()`：当点击元素的时候调用
`dblclick()`：当双击元素的时候调用
`keydown()`：当键盘按钮被按下时调用
`keyup()`：当键盘按钮被松开时调用
`keypress()`：当键盘按钮被按下时调用（必须插入字符才能被调用）
`mousedown()`：当鼠标指针移动到元素上方，并按下鼠标按键时调用
`mouseup()`：当在元素上放松鼠标按钮时调用，常与mousedown()一起使用
`mousemove()`：当鼠标指针在指定元素上移动时调用
`submit()`：当提交表单的时候调用

**`jQuery`是为处理`HTML`事件而特别设计的，当遵循以下原则时，代码会更容易维护：**
- 把所有`jQuery`代码置于事件处理函数中
- 把所有事件处理函数置于文档就绪事件处理器中
- 把`jQuery`代码置于单独的`.js`文件中

####关于`DOM`
相比原生`javascript`，`jQuery`拥有更为强大的可操作`HTML`元素和属性的方法。

**查找`HTML`元素**
- `$("#id")`
- `$(".class")`
- `$("tag")`

**对元素的操作**
- `append()`：在被选元素的结尾插入内容
- `prepend()`：在被选元素的开头插入内容
- `after()`：在被选元素之后插入内容
- `before()`：在被选元素之前插入内容
- `remove()`：删除被选元素（及其子元素）
- `empty()`：从被选元素中删除子元素

**对属性的操作**
- `attr()`：设置或返回所选元素的属性和值
- `removeAttr()`：从所选元素中移除指定的属性
- `addClass()`：为所选元素添加指定的类名
- `removeClass()`：为所选元素删除全部或指定的类
- `hasClass()`：判断所选元素是否拥有指定的类

**对文本的操作**
- `text()`：设置或返回所选元素的文本内容
- `html()`：设置或返回所选元素的内容（包括`HTML`标记）
- `val()`：设置或返回表单字段的值

**对`CSS`的操作**
- `css()`：设置或返回所选元素的样式属性
- `height()`：设置或返回所选元素的高度
- `width()`：设置或返回所选元素的宽度




