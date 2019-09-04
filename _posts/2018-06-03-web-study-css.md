---
layout: post
title:  "CSS"
date:   2018-06-03
categories: Web前端
tags: web
excerpt: Web前端
---

* content
{:toc}

#### `CSS`

**`Cascading Style Sheet`，层叠样式表，将网页内容和显示样式分离，提高程序性能。**

_它是一种专门描述结构文档的表现方式的文档，主要用于网页风格设计，包括字体大小、颜色、以及元素的精确定位。在传统的`web`网页设计里，使得`css`能让单调的`html`网页更富表现力。_

<hr />
**`css`的引入方式**

`css`可以控制`html`文档的显示，但是控制文档显示之前，首先应在需要显示的`html`文档中引入`css`样式表，`html`提供了以下四种引入方式：

（1）内联样式：将样式内联定义到具体的`html`元素上，利用元素的`style`属性实现，通用用于精确控制一个`html`元素的表现。

    <!-- 内联样式：将css代码写在html具体的元素的style属性内 -->
    <p id="p1" style="color: red; font-size: 16px">内联样式</p>

（2）内部样式：通常在`html`文档头部定义样式单部分来实现，这种方式下每批`css`样式只控制一份`html`文档。

    <!-- 内部样式：将css代码写在<head>里的<style>标签内实现 -->
    <style type="text/css">
    	#p2{
    		color: blue;
    		font-size: 20px;
    	}
    </style>

（3）外链样式：样式文件和`html`文档分离，样式文件需要额外引入，这种方式下每批`css`样式能控制多份`html`文档（最常用）。

    <!-- 外链样式：利用link标签引入，使用频率最高 -->
    <link rel="stylesheet" type="text/css" href="outer.css" />

（4）导入外部样式：和第三种方式类似，只是使用`@import`来引入外部样式表文件。

    <!-- 导入外部样式：与link方法类似，语法不通，在<style>标签内使用 -->
    <style type="text/css">
    	@import "outer.css'";
    	@import url("outer.css");
    </style>

优先级：内联样式`style`> 内部样式 > 导入外部样式`import` > 外链样式`link`

<hr />
**`css`常用选择器介绍**

定义`css`样式的语法总遵循如下格式：

    Selector{
    	property1: value1;
    	property2: value2;
    }
    
    Selector：选择器，决定该样式的定义对哪些元素起作用
    {property:value...}：属性定义，决定这些样式起怎样的作用（字体、颜色、布局等）

**标签选择器**：声明哪种标签会使用该`css`样式

    /* E{....}，其中E代表有效的html元素 */
    a{
    	background-color: blue;
    	color: red;
    }

**`class`选择器**：声明特定`class`值的标签会使用该`css`样式（一个标签可以设置多个`class`值）

    /* [E].classValue{....}，其中E表示html元素，当E存在时，指定的范围是标签为E且属性class的值为classValue，不存在时，范围是标签属性class的值为classValue */
    .p2{
    	background-color: yellow;
    	color: gray;
    }

**`id`选择器**：声明特定id值的标签会使用该`css`样式（一个标签只能设置一个`id`值）

    /* [E]#idValue{....}，同class选择器概念，E可存在或不存在 */
    #id1{
    	background-color: gray;
    	color: white;
    }

**组合选择器**：将具有相同`css`样式的选择器，一次性声明（不限于标签选择器，`class`选择器和`id`选择器也可以组合）

    /* Selector1, Selector2, Selector3{....}，Selector都是有效的选择器，可以是标签选择器、class选择器、id选择器等 */
    span, b, #id1{
    	color: red;
    }

**嵌套选择器**：也叫关联选择器（不只是标签选择器能嵌套，`class`选择器和`id`选择器也可以）

    /* Selector1 Selector2{....}，Selector都是有效的选择器，表示当前需要设定样式的范围是Selector1选择器下所有的Selector2选择器*/
    div p{
    	background-color: green;
    	color: white;
    }

<hr />
**常用的`css`属性介绍**

**字体**
`font-family`：规定文本的字体系列，如`"serif"`、`"sans-serif"`等
`font-size`：规定文本的字体尺寸
`font-style`：规定文本的字体样式，主要有`normal`,`italic`,`oblique`
`font-weight`：规定字体的粗细，主要有`normal`,`bold`,自定义粗细

**文本**
`color`：设置文本颜色
`letter-spacing`：设置字符间距（每个字母间的间距）
`line-height`：设置文本行高
`text-align`：设置文本的对齐方式，只有`left`, `right`, `center`
`text-decoration`：设置文本的装饰效果，主要有`overline`（上划线）, `underline`（下划线）, 		`line-through`（删除线）
`text-indent`：设置文本看首行缩进
`text-transform`：设置文本的大小写，主要有`uppercase`, `lowercase`, `capitalize`
`word-spacing`：设置单词间距

**边框**
`border`：在一个声明中设置所有的边框属性
`border-color`：设置四条边框的颜色
`border-style`：设置四条边框的样式，只要有`dotted`, `solid`, `double`, `dashed`等值
`border-width`：设置四条边框的宽度
边框分为：`border-left`、`border-right`、`border-top`、`border-bottom`
`border-left`：在一个声明中设置所有左边框属性，对应还有`border-right`等
`border-left-color`：设置左边框颜色
`border-lelft-style`：设置左边框样式
`border-left-width`：设置左边框宽度
    
可以将属性一次性写在一起，更方便
`border: 10px red solid;`

**背景**
`background`：在一个声明中设置所有的背景属性
`background-attachment`：设置背景图像是否固定或者随着页面的其余部分滚动，主要有`fixed`和`scroll`两个值
`background-color`：设置元素的背景颜色
`background-image`：设置元素的背景图片，主要有`url`和`none`两个属性
`background-position`：`px`, `%` 设置背景图像的开始位置，可以指定`top` `left`等，也可以指定具体的像素位置
`background-repeat`：设置是否及如何重复背景图像，主要有`repeat`, `repeat-x`, `repeat-y`, `no-repeat`

**列表**
`list-style`：在一个声明中设置所有的列表属性，设置成`none`可以去掉`ul`中的原点等属性值
`list-style-image`：将图像设置为列表项标记，主要有`url`值
`list-style-position`：设置列表项标记的放置位置，主要有`outside`和`inside`两个值
`list-style-type`：设置列表项标记的类型，主要有`disc`, `circle`, `square`, `decimal`等，不能和`list-style-image`同时使用

**表格**
`border-collapse`：设置是否把表格边框合并为单一的边框，值为`collapse`
`border-spacing`：设置分割单元格边框的距离，与`border-collapse`不能同时使用
`caption-side`：设置表格标题的位置
`empty-cells`：设置是否显示表格中的空单元格，值为`hide`, `show`

**常用伪类别属性**
`<a>`超链接标签
	`a:link` 超链接的普通样式
	`a:visited` 被点击过的超链接样式
	`a:hover` 鼠标指针经过超链接上时的样式
	`a:active` 在超链接上单击时，既"当前激活"时超链接的样式
    
块级标签->行级标签：`display:inline`
行级标签->块级标签：`display:block`
注：行级标签是默认情况下是不能设置宽度和高度的，如果要设置，需要把行级标签变成块级标签
    
<hr />
**盒子模型**

_我们可以把页面中的元素都可以看作一个盒子，占据着一定的页面空间，这些占据的空间往往比单纯的内容要大，换句话说，我们可以调整盒子的边框和距离的参数来调整盒子的位置。_

盒子宽度：`content`+`padding`+`border`+`margin`

因此我们可以利用好盒子的这些属性，就能很好的实现各种各样的排版效果。

`border`属性主要有3个，`border-color`, `border-width`, `border-style`，通常在设置`border`时常常将3个属性进行很好的配合，才能达到良好的效果。

`padding`用于控制`content`与`border`之间的距离。
`padding`：一次性将四个边距全部设置（上右下左，顺时针）
`padding-top`：上边距
`padding-bottom`：下边距
`padding-left`：左边距
`padding-right`：右边距

`margin`指的是元素与元素之间的距离。
`margin`：一次性将四个边距全部设置（上右下左，顺时针）
`margin-top`：上边距
`margin-bottom`：下边距
`margin-left`：左边距
`margin-right`：右边距
    
注：

- 两个行级元素之间的距离是margin-left和margin-right两者的和，两个块级元素之间的距离不是margin-top和margin-bottom的和，而是两者之中的较大值。
- 其实margin除了设置正数以外，也可以设置负数，当设置为负数时，会使得块向反方向移动，甚至覆盖在另外的块上。
- 当块之间是父子关系，通过设置子块的margin为负数时，可以使得子块从父块中"分离出来"

<hr />
**元素的定位**

网页中各个元素都必须有自己的位置，从而搭建出整个页面的结构。
    `float`：值为`left`, `right`或者默认值`none`，当设置了元素向左浮动或向右浮动时，元素会向其父元素的左侧或右侧靠近
    `clear`：设置块元素的`clear`属性清除对`float`的影响，值为`left`, `right`, `both`
    `position`：制定块的位置，即块相对于其父块的位置和相对它自身应该在位置，值有`absolute`, `fixed`, `relative`, `static`
    当将子块的`position`设置为`absolute`时，子块已经不再从属于父块，其边框设置的距离是相对页面`body`的距离，而不是父块的距离
    当将块的`position`参数设置为`relative`时，与将其设置为`absolute`时完全不同，这时子块时相对于自身在父块的原先位置来进行定位的。

定位资料参考：http://www.cnblogs.com/dolphinX/archive/2012/10/13/2722501.html


