---
layout: post
title:  "JQuery"
date:   2018-06-06
categories: Web前端
tags: web
excerpt: Web前端
---

* content
{:toc}

#### `HTML`

**`Hyper Text Markup Language`，超文本标记语言，不是一种编程语言，而是一种标记语言**

_思想：网页中有很多数据，不同的数据可能需要不同的显示效果，一个标签相当于一个容器，想要修改容器内数据的样式，只需要改变容器的属性值，就可以实现容器内数据样式的变化。_

**语言结构介绍：**

    <!-- 声明文档页面使用的html版本，当前是html5 -->
    <!DOCTYPE html>
    
    <!-- html文档的根元素标签，表示html文档的开始和结束 -->
    <html>
    	<!-- html文档的头部标签 -->
    	<head>
    		<!-- 定义文档标题 -->
    		<title>html学习</title>
    
    		<!-- 
    		用于html页面的元信息
    		http-equiv：指定元信息的名称，该属性指定的名称具有特殊意义，它可以向浏览器传回一些有用的信息，帮助浏览器正确地处理网页内容。
    		name：指定元信息名称，该名称可以随意指定
    		content：指定元信息的值
    		 -->
    		<!-- 指定文档的字符编码 -->
    		<meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
    		<!-- 3s后会自动跳转到baidu主页 -->
    		<meta http-equiv="refresh" content="3;url=http://www.baidu.com"/> 
    		<!-- 指定作者 -->
    		<meta name="author" content="author_name"/>
    		<!-- 指定关键字，用逗号隔开（便于搜索引擎进行搜索） -->
    		<meta name="keywords" content="关键字1，关键字2，关键字3"/>
    		<!-- 对关键字进行描述 -->
    		<meta name="description" content="对关键字的描述...">
    
    		<!-- 链接外部js资源文件 -->
    		<script src="theme.js"></script>
    		<!-- 包含js脚本 -->
    		<script type="text/javascript">
    			// js代码
    		</script>
    
    		<!-- 链接外部css资源文件 -->
    		<link rel="stypesheet" type="text/css" href="theme.css"/>
    		<!-- 定义内部css样式 -->
    		<style type="text/css">
    			/* css代码 */
    		</style>
    	</head>
    
    	<!-- html文档主体标签 -->
    	<body>
    	</body>
    </html>

**块级标签**
显示为"块"状，浏览器会在其前后显示折行。常用的块级元素包括：`<p>`, `<h1>~<h6>`, `<div>`, `<ul>`等

**标题标签**

    <!-- 标题标签，从h1到h6依次文字减小 -->
    <h1>一级标题</h1>
    <h2>二级标题</h2>
    <h3>三级标题</h3>
    <h4>四级标题</h4>
    <h5>五级标题</h5>
    <h6>六级标题</h6>

**段落标签**

    <p>同一个世界，同一个梦想</p>
    <p>梦想还是要有的，万一实现了呢？</p>

**水平线标签**

    <!-- <hr/> size从1-7，越来越粗 -->
    <hr/>

**列表**

    <!-- ol：有序列表 type设置排序方式 1默认，还有a,i.. -->
    <ol type="a">
    	<li>中国</li>
    	<li>日本</li>
    	<li>韩国</li>
    </ol>
    
    <!-- ul：无序列表 type：circle（空心圆）,disc（实心圆）,square（实心方块），默认desc -->
    <ul type="circle">
    	<li>苹果</li>
    	<li>香蕉</li>
    	<li>橘子</li>
    </ul>
    
    <!-- dl：definition list，定义列表，最常用 -->
    <!-- dl, dt, dd, 可以将or和ul放在dd里面 -->
    <dl>
    	<dt>亚洲</dt>
    		<dd>中国</dd>
    		<dd>日本</dd>
    		<dd>朝鲜</dd>
    	<dt>欧洲</dt>
    		<dd>英国</dd>
    		<dd>法国</dd>
    		<dd>德国</dd>	
    </dl>

**分区标签**

    <!-- div标签一般当作结构化块状元素使用，一般最常用的用途是对网页进行整体分块布局，即当容器来使用 -->
    <div id="fruit">
    	<p>苹果</p>
    	<p>香蕉</p>
    	<p>橘子</p>
    </div>
    <div id="country">
    	<p>中国</p>
    	<p>日本</p>
    	<p>朝鲜</p>
    </div>

**行级标签**

按行逐一显示，前后不会自动换行，常用的行级标签包括：`<b>`, `<i>`, `<sub>`, `<sup>`等

    <!-- 定义粗体文本 -->
    <b>粗体文本</b>
    <!-- 定义倾斜文本 -->
    <i>倾斜文本</i>
    <!-- 效果和b类似，语气较强 -->
    <strong>粗体文本</strong>
    <!-- 效果和i类似，语气较强 -->
    <em>倾斜文本</em>
    <!-- 定义小号文本 -->
    <small>小号文本</small>
    <!-- 定义下标文本 -->
    H<sub>2</sub>o
    <!-- 定义上标文本 -->
    10<sup>2</sup>
    <!-- 定义文本显示方向，内有dir属性，只能取值ltr从左到右或rtl从右到左 -->
    <bdo dir="rtl">文本内容</bdo>
    
    <!-- 
    超链接标签
    href：指定超链接所关联的另一个资源
    target：指定框架集中的哪个框架来装载另一个资源，该属性值有_self, _blank, _top, _parent四个值，分别代表使用自身、新窗口、顶层框架、父框架来装载新资源
     -->
    <a href="超链接地址" target="目标窗口">点击</a>
    
    <!-- 图像标签 -->
    <img src="图片地址" alt="提示文字"/>
    
    <!-- span标签：内部放文本或者行级标签 -->
    <span>文本等行级内容</span>
    
    <!-- 换行标签 -->
    <br/>
    
    <!-- 常用的特殊符号 -->
    &nbsp;	<!-- 空格 -->
    &gt;	<!-- 大于号(>) -->
    &lt;	<!-- 小于号(<) -->
    &quot;	<!-- 引号(") -->
    &copy;	<!-- 版权符号(©) -->



**框架**
`frameset`框架集
创建框架页面的步骤：

- 创建各个子窗口对应的`html`文件
- 创建整个框架文件，分别引用子窗口文件

框架的使用

    <!-- 
    frameset：框架集标签，不能与body标签同时使用，除非与noframes标签联合使用时
    将浏览器分割成多个框架页，来加载多个html页面
    frame：框架标签
    cols：pixels, %, * 定义框架集中列的数目和尺寸
    rows：pixels, %, * 定义框架集中行的数目和尺寸
    noresize：设置框架尺寸不可调整
    border：设置框架边框宽度
    -->
    <frameset rows="25%,*" border="1" noresize="noresize">
    	<frame src="top.html">上边/frame>
    	<frameset cols="25%,*">
    		<!-- 如果希望点击左边框架的超链接，右边框架显示超链接内容，可以将左边超链接a标签的target设置成右边框架的名称即可 -->
    		<frame src="left.html" name="leftFrame">左边</frame>
    		<frame src="right.html" name="rightFrame">右边</frame>
    	</frameset>
    	
    	<!-- noframe标签为那些不支持框架的浏览器显示文本，noframes元素位于frameset内部 -->
    	<noframes>
    		<body>
    			您的浏览器无法处理框架！
    		</body>
    	</noframes>
    </frameset>

`iframe`内嵌框架

    <!-- 
    iframe：内嵌框架，在body标签内部
    frameborder：0, 1 规定是否显示框架周围的边框
    name：规定iframe的名称
    scrolling：yes(显示), no(不显示), auto(内容超过框架则显示，否则不显示) 规定是否在iframe中显示滚动条
    scr：规定在iframe中显示的文档的url
    width：框架宽度
    height：框架高度
     -->
    <body>
    	<!-- <iframe src="引用页面地址" name="框架标识名" frameborder="边框" scrolling="是否显示滚动条"> -->
    
    	<!-- 和frameset类似，如果希望点击iframe外的超链接，iframe中显示相应的网页，可以将超链接a标签的target设置成iframe的名称即可 -->
    	<iframe src="http://www.baidu.com" name="contentFrame" width="100%" height="400px"></iframe>
    	<p><a href="http://www.sina.com.cn/" target="contentFrame">新浪</a></p>
    	<p><a href="http://www.baidu.com/" target="contentFrame">百度</a></p>
    	</iframe>
    </body>


**表格**

使用场景

- 主要用于规则的数据显示；
- 适当的可以在表单页面中使用；

使用表格标签进行页面布局的缺点

- 代码量比较大，页面浏览速度比较慢；
- 层次结构比较复杂，不易于维护和改版；
- 不利于搜索引擎搜索查找数据；


    <!-- 
    定义表格的开始和结束
    cellpadding：单元格边框和内容之前的距离
    cellspacing：单元格和单元格之间的距离
     -->
    <table border="1" cellspacing="0">
    	<!-- 定义表格的标题 -->
    	<caption>我喜欢的NBA球队</caption>
    	
    	<!-- 定义表格头 -->
    	<thead>
    		<!-- 定义表格行，该元素内只能包含th标签和td标签 -->
    		<tr>
    			<!-- 定义表格页眉的单元格 -->
    			<th>球队名称</th>
    			<th>老板</th>
    			<th>当家球星</th>
    		</tr>
    	</thead>
    	
    	<!-- 定义表格的主体 -->
    	<tbody>
    		<tr>
    			<!-- 
    			定义单元格，包含两个主要的属性
    			colspan：单元格跨多少列
    			rowspan：单元格跨多少行
    			 -->
    			<td>骑士</td>
    			<td>丹尼尔·吉尔伯特</td>
    			<td>勒布朗·詹姆斯</td>
    		</tr>
    		<tr>
    			<td>勇士</td>
    			<td>乔·拉科布</td>
    			<td>斯蒂芬·库里</td>
    		</tr>
    		<tr>
    			<td>马刺</td>
    			<td>皮特·霍尔特</td>
    			<td>科怀·伦纳德</td>
    		</tr>
    	</tbody>
    	
    	<!-- 定义表格尾部 -->
    	<tfoot>
    		<tr>
    			<td colspan="3">总计3支球队</td>
    		</tr>
    	</tfoot>
    	
    </table>


**表单**
基本语法

    <!-- 
    action：指定表单提交后由服务器上的哪个处理程序进行处理
    enctype：用于指定表单数据的编码方式
    method：指定向服务器提交的方式 get post
     -->
    <form action="表单提交地址" method="提交方法" target="打开方式">
    	<!-- 文本框、按钮等表单元素 -->
    </form>

常见的表单元素使用

    <!-- 
    		input元素中常用属性：
    		checked：设置单选框、复选框初始状态是否处于选中状态，只有当type属性为checkbox或radio时才可指定
    		disabled：设置首次加载时禁用此元素，当type为hidden时不能指定该属性
    		maxlength：指定文本框中所允许输入的最大字符数
    		readonly：指定该文本框内的值不允许修改（可用js脚本修改）
    		size：指定该元素的长度
    		src：指定图像域所显示的图像url，只有当type的值为image时才可以指定该属性
    		 -->
    
    		<!-- text，单行文本框 -->
    		单行文本框：<input type="text" maxlength="10" size="4" /><br/>
    
    		<!-- password，密码输入框 -->
    		密码输入框：<input type="password" disabled="disabled"/><br/>
    
    		<!-- hidden，隐藏域 -->
    		隐藏域<input type="hidden"/><br/>
    
    		<!-- radio，单选框 -->
    		单选框：男<input type="radio" name="sex" value="0" />
    			   女<input type="radio" name="sex" value="1" checked="checked" /><br/>
    			
    		<!-- checkbox，复选框 -->
    		复选框：篮球<input type="checkbox" name="hobby" value="0" /> 
    			   足球<input type="checkbox" name="hobby" value="1" />
    			   排球<input type="checkbox" name="hobby" value="2"><br/>
    
    		<!-- image，图像域，可以指定width和height属性，有submit按钮的功能，会提交表单数据 -->
    		图像域：<input type="image"/><br/>
    
    		<!-- file，文件上传域 -->
    		文件上传：<input type="file"/><br/>
    
    		<!-- submit、reset、button，提交、重置、普通按钮 -->
    		提交按钮：<input type="submit" value="提交按钮"/><br/>
    		重置按钮：<input type="reset" value="重置按钮"/><br/>
    		普通按钮：<input type="button" value="普通按钮"/><br/>

使用`button`定义按钮

    <!-- 
    button按钮与input按钮相比，提供了更强大的功能和更丰富的内容
    disabled：指定是否禁用此元素，该属性的值只能是disabled或者省略
    name：指定按钮的唯一名称
    type：指定按钮属于哪种按钮，只能是button、reset、submit
     -->
    <button type="按钮类型" name="按钮名称">
    	普通文本、格式化文本、图像
    </button>
    
    提交按钮：<button type="submit"><b>提交按钮</b></button><br/>
    重置按钮：<button type="reset"><i>重置按钮</i></button><br/>
    普通按钮：<button type="button">普通按钮</button>

使用`label`定义标签

    <!-- 
    label元素不会向用户呈现任何特殊效果，不过它为鼠标用户改进了可用性。如果在label元素内点击文本，就会触发，浏览器会自动将焦点转到和标签相关的表单控件上。
    for：规定label绑定到哪个表单元素，值为表单元素的id
    form：规定label字段所属的一个或多个表单
     -->
    <!-- <label>文本</label> -->
    <label for="text">单行文本框：</label><input type="text" id="text"/>

**列表菜单和下拉菜单**

    <!-- 
    select标签常用属性：
    disabled：指定是否禁用此元素，该属性的值只能是disabled或者省略
    mutiple：设置该列表框是否允许多选
    size：指定该列表内同时显示多少个列表项
     -->
    <!-- 
    基本语法：
    <select name="指定列表名称" size="行数">
    	<option value="选项值" selected="selected">...</option>
    </select> 
    -->
    <!-- 列表菜单：多选项展示，可多选 -->
    <select size="3" multiple="multiple" id="country">
    	<option value="0">中国</option>
    	<option value="1">美国</option>
    	<option value="2">日本</option>
    	<option value="3">韩国</option>
    </select><br/>
    
    <!-- 下拉菜单 -->
    <select id="city">
    	<option value="0">北京</option>
    	<option value="1">上海</option>
    	<option value="2">武汉</option>
    	<option value="3">广州</option>
    </select><br/>
    
    <!-- 
    在<select>标签内，只能包含如下两种子元素：
    <option>：用于定义列表框选项或菜单项，它的常用属性如下：
    	disabled：指定禁用该选择，该属性的值只能是disabled或省略
    	selected：指定该列表初始状态是否处于选中状态，值只能为selected
    	value：指定该选项对应的请求参数值
    <optgroup>：用于定义列表项或菜单项组，它的常用属性如下：
    	label：指定该选项组的标签，必需
    	disabled：禁用该选项组里的所有选项，该属性值只能为disabled或省略
    -->
    <select>
    	<optgroup label="一线城市">
    		<option>北京</option>
    		<option>上海</option>
    		<option>广州</option>
    	</optgroup>
    	<optgroup label="二线城市">
    		<option>杭州</option>
    		<option>武汉</option>
    		<option>南京</option>
    	</optgroup>
    </select>

**多行文本框**

    <!-- 
    textarea：多行文本框，常用属性如下：
    cols：指定文本框的宽度，必填
    rows：指定文本框的高度，必填
    readonly：指定该文本框只读，该属性的值只能是readonly或省略
     -->
    <!-- 
    基本语法：
    <textarea name="..." cols="列宽" rows="行宽">
    文本内容
    </textarea> 
    -->
    <textarea name="content" cols="50" rows="5" readonly="readonly">
    1) 用户可通过各种已有和未来新增的渠道注册账号及加入付费使用。 
    2) 在用户使用具体某种方式加入付费会员时，须阅读并确认相关的用户协议和使用方法。
    </textarea>

**`html`多媒体**

`web`上的多媒体指的是音效、音乐、视频和动画，现代网络浏览器已经支持很多多媒体格式。常见的视频格式有`avi`,` wmv`, `mpg/mpeg`, `mov`, `rm/ram`, `mp4`等，常用的音频格式有`mid/midi`, `rm/ram`, `wav`, `wma`, `mp3/mpga`等。

在`html5`之前，主要提供两种元素来进行多媒体的展示，一个是`<embed>`标签，另一个是`<object>`标签。

    <!-- 
    embed是html5中新标签，定义嵌入的内容，比如插件，常用属性：
    height：设置嵌入内容的高度
    width：设置嵌入内容的宽度
    src：设置嵌入内容的url
    type：设置嵌入内容的类型
    
    在html5中提供了audio（音频）和video（视频）标签来进行音频和视频的播放，使用比较简单，功能更强大。
     -->
    
    <!-- embed播放音频 -->
    <!-- <embed src="/Users/wangzhao/Music/网易云音乐/电台节目/这个少女不太冷丶 - 牵丝戏.mp3" width="0" height="0" autostart="false" loop="true"></embed> -->
    
    <!-- embed播放flash视频 -->
    <embed src="xxx.swf" width="200" height="200" loop="true" quality="high" PLUGINSPAGE="http://www.macromedia.com/shockwave/download/index.cgi?P1_Prod_Version=ShockwaveFrash"></embed>
    
    
    <!-- object标签 -->
    <!-- 
    可以使用<object>标签来给浏览器加载插件，通过加载的插件来播放音频和视频
    微软开发，对IE兼容性很好，对其他浏览器兼容一般
     -->
     <object data="/Users/wangzhao/Music/网易云音乐/电台节目/这个少女不太冷丶 - 牵丝戏.mp3">
     	<param name="src" value="/Users/wangzhao/Music/网易云音乐/电台节目/这个少女不太冷丶 - 牵丝戏.mp3">
     	<param name="autoplay" value="false">
     </object>




