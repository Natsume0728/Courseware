# HTML

<!-- TOC depthFrom:2 orderedList:false -->

- [web基础知识](#web基础知识)
    - [web与internet的关系](#web与internet的关系)
    - [internet上的应用程序都会分成两类](#internet上的应用程序都会分成两类)
    - [web运行原理](#web运行原理)
- [html快速入门](#html快速入门)
- [HTML的文档结构](#html的文档结构)
- [文本标记(重点***)](#文本标记重点)
    - [标题元素](#标题元素)
    - [段落标记](#段落标记)
    - [换行标记](#换行标记)
    - [特殊字符(实体)](#特殊字符实体)
    - [分割线，水平线](#分割线水平线)
    - [预格式化](#预格式化)
    - [文本样式标签](#文本样式标签)
    - [分区元素--不写样式的分区元素，是看不见的](#分区元素--不写样式的分区元素是看不见的)
    - [元素的显示方式](#元素的显示方式)
- [图形图像](#图形图像)
    - [图像的使用 \<img>](#图像的使用-\img)
- [URL](#url)
- [链接](#链接)
    - [语法](#语法)
    - [a标签的其它表现形式](#a标签的其它表现形式)
    - [锚点](#锚点)
- [表格](#表格)
    - [不规则的表格](#不规则的表格)
    - [表格的复杂应用](#表格的复杂应用)
- [列表（重点*******）](#列表重点)
- [结构标签](#结构标签)
- [表单\*\*\*\*重点\*\*\*\*\*](#表单\\\\重点\\\\\)
    - [form表单详解](#form表单详解)
- [浮动框架](#浮动框架)

<!-- /TOC -->

---

## web基础知识

HTML:泛指前端网页技术,  
2014年9，html4.0升级html5.，简称**h5**,  
Html5 大前端技术;  
html4.01在1999.12月发布;  
xhtml1.0 在2000.1月发布，语法更严谨
\<img/> \<img>

### web与internet的关系

internet:全球性计算机互联网络,  
俗称 互联网，因特网，交换网，交际网;  
www服务:world wide web 万维网;  
ftp:文件的上传下载的服务;  
Email:电子邮件的服务;  
telnet：远程登陆的服务;  
BBS：电子公告板，俗称论坛;  
**以上都是运行在internet应用程序**。

### internet上的应用程序都会分成两类

- C/S  
client 客户端 ： 王者荣耀  
server服务器 ： QQ.exe  
- B/S  
browser浏览器 ：所有的网站  
server服务器 ： 网页版微信  

**C/S结构和B/S结构的区别**：

- C/S需要升级  
- B/S不需要升级

### web运行原理

web：  
运行在internet上的一种B/S结构的应用程序，俗称网站；  
internet:为web运行提供了网络环境；  

web运行的原理：  
基于**浏览器**和**服务器**，以及**通信协议**来实现数据的传输和展示；  

**通信协议**：  
规范了数据是如何打包和传递的；  
网页的通信协议 ： `http://`  `https://`  

**服务器**:  

- 功能:
  - 存储数据
  - 接收用户的请求，并且给出响应
  - 提供程序的运行环境
  - 具备一定的安全功能
- 服务器产品:  
  - Apache--php
  - TOMCAT--java
  - IIS .net
- 服务器端技术
  - nodejs
  - java
  - php  
  - .net
  - Python

**浏览器**:  

- 功能  
  - 代表用户发送请求
  - 作为html，css和js的解析器
  - 以图形化的界面展示给用户看
- 浏览器产品
  - safari
  - chrome
  - firefox
  - opera
  - ie
- 浏览器端的技术
  - html5  
  - css3  
  - javascript  

---

## html快速入门

1. 什么是html  
HyperTexts Markup Language  
超文本标记语言  
标记：超文本组成形式，<关键字>，具体独特的功能  
2. html的特点  
![HTML__001.jpg](https://i.loli.net/2019/06/29/5d164ae166c3519968.jpg)  
   - 以.html或者.htm为后缀
   - 由浏览器解析执行
   - 用<>来定义标记
   - 可以嵌套js脚本  
3. html语法  
   - 标记  
标记，元素，标签，节点  
<关键字>  
标签具备一些功能  
标记分为两类
     1. 双标记（封闭类型标记）  
<关键字>\</关键字>
双标记成对出现，有开有关  
ex:\<a>\</a>  
     1. 单标记(非封闭类型标记，空标记)  
<关键字>  或者  <关键字/>  
ex：\<input/>  \<br/>  \<img/>  
   - 属性和值  
通过属性和值，对标签进行修饰  
<标签 属性1="值1"  属性2="值2" ...></标签>  
     - 标准属性，  
     通用属性,所有标签都有的属性  
id:定义元素在页面中唯一的标识  
title：鼠标悬停在元素生显示的文本  
style：css中，定义内联样式  
class：css中，引用类选择器时使用  
     - 专有属性，  
     只针对一个标签起作用的属性  
   - 注释  
不会被浏览器解析运行的部分  
一般编写代码说明  
\<!-- -->
注释不能嵌套注释  
注释不能写在标签内部  

>学习html就三步  
1.学习固定标签关键字，及功能；  
2.学习固定的嵌套关系；  
3.学习固定的属性及其值。  

---

## HTML的文档结构

html文档的构成  

1. 文档类型声明  
\<!doctype html>  
告诉浏览器，解析运行本篇代码，使用h5的规则解析  
1. 网页的结构  
\<html>\</html>
表示网页的开始和结束。  
一个html文件中只能有一对html标签。  
1. head标签，**定义网页的信息**  
   1. \<meta> **元数据标签**  
\<meta charset="utf-8">  
\<meta name="description" content="描述内容">  
\<meta name="Keywords" content="关键字">  
   2. head中其它标签  
\<title>\</title> 网页标题  
\<script>\</script> 编写js或者引用js文件  
\<style>\</style> css中定义内部样式  
\<link>引入外部css样式  
1. body元素  
指定网页的主体  
\<body>\</body>  
属性：  
bgcolor ==> body 的背景颜色，取值颜色合法值  
text ==> body 的文本颜色，取值颜色的合法值  

---

## 文本标记(重点***)

### 标题元素

在页面中以醒目的方式显示文本  
\<h1>\</h1>  
\....  
\<h6>\</h6>  

特点：  

1. 字体大小有变化  h1最大，h6最小  
2. 字体加粗  
3. 单独成行，上下有垂直间距  

属性：  
align ==>设置标记内容水平对齐方式  
      取值：left/center/right

### 段落标记

\<p>\</p> 以突出的形式表示一段文字  

特点：  

1. 单独成行
2. 上下有垂直间距  
属性：align:left/cener/right  

### 换行标记

**空格折叠现象**：  
在html中，文本中不管有多少个空格和回车，都会被浏览器解析成一个空格显示。  
\<br> 或者 \<br/>  

### 特殊字符(实体)  

- \&nbsp;  空格
- \&lt;   <  
- \&gt;  >  
- \&times； X
- \&reg; 商标注册 ®
- \&copy；版权 ©
- \&yen;  

### 分割线，水平线

\<hr>  或者  \<hr/>  

属性  

- size="5px"  取值px为单位的数字，水平线的粗细
- width="50%"  取值px或者%,水平线的宽度
- align="left"   left/center/right
- color="blue" 取值为合法颜色值  

### 预格式化

\<pre>\</pre>  
保留html代码中的回车和空格效果  

### 文本样式标签

- \<em> \</em>         \<i> \</i>   斜体
- \<strong> \</strong>  \<b> \</b>  加粗
- \<del> \</del>         \<s> \</s>  删除线
- \<u> \</u>  下划线
- \<sup> \</sup> 上标
- \<sub> \</sub> 下标

### 分区元素--不写样式的分区元素，是看不见的

- 块分区 \<div> \</div>  
用于页面布局  
- 行分区 \<span> \</span>  
为文本添加样式的时候用span

### 元素的显示方式

- 块级元素  
元素独立成行，在页面中从上往下排列  
ex:h1~h6  p  div  pre  
- 行内元素(行级元素)  
多个行内元素在一行中显示，从左往右排列  
ex:span i em strong b u sub sup del s  
- 行内块  
表现方式是行内元素(多个行内块可以共用一行)  
但是具有块级元素的其它特征(宽高，边距)  
ex:input
- table  

---

## 图形图像

>\<img/> 或者 \<img>  

### 图像的使用 \<img>  

属性：  

- src：source 源，资源路径
- alt： 图片错误时，显示的文本
- title：鼠标悬停时显示的文本
- width：设置图片的宽度
- height：设置图片的高度

>如果设置宽高比，不符合图片原始宽高比,图片会产生失真效果。  
解决图片失真效果：  
**一般情况下，width和height只设置一个，让另外一个自动适应**。

---

## URL

>Uniform Resource Locator 统一资源定位器;  
就是路径。

- 绝对路径  
完整的路径:  
协议+主机名称+文件目录结构+文件具体的名称;  
使用场合：  
使用网络资源的时候，使用绝对路径。  

使用网络资源图片：  
优点：节省服务器本地存储空间  
缺点：资源不稳定  

绝对路径使用本地的资源，是从最高盘符开始查找  
c:\img\08.png  
但是本服务器资源，在项目中，不能用绝对路径  

- 相对路径  
使用本服务器资源，用相对路径  
  - 同级目录资源  
直接使用资源名称 src="08.png"
  - 兄弟文件夹的子元素  
直接使用兄弟文件夹的名称，在用/调用资源名称
src="img/08.png"
  - 父级目录中资源  
先使用../返回上一级，在引用资源名称
src="../08.png"

---

## 链接

### 语法

\<a href=""> \</a>  

属性：  

- href 链接路径  
- target 指定打开链接的方式  
  - _self 默认值，在当前页面打开新网页
  - _blank 在新的页面打开网页

### a标签的其它表现形式

- 新建邮件，配合windows的邮件软件使用  
     \<a \href=`"mailto:cheng@t.com"`>发邮件\</a>
- 执行js
    \<a href="javascript:show()">执行js\</a>
- 下载
    \<a href="1.zip">下载\</a>
- 返回页面顶部  
    \<a href="#">返回页面顶部\</a>

### 锚点

>锚点是网页中的一个记号,  
可以通过超链接的方式，链接到锚点，让页面跳转到锚点位置显示。

使用锚点  

- 定义锚点
  - 第一种方式： 任何标签的id中写锚点名称;  
  \<Any id="锚点名称"> </ Any >
  - 第二种方式： a标签的name属性中写锚点名称;  
  \<a name="锚点名称">\</a>
- 链接到锚点  
  \<a href="#锚点名称">\</a>  
- 链接到其它页面的锚点  
  \<a href="其它页面的url#锚点名称">\</a>  
  \<a href="02_a.html#hl">葫芦娃\</a>

---

## 表格

早期table用于布局,  
由于效率低下，后来被淘汰，使用div+css的布局,  
表格现在就一个单纯的作用---显示数据。  

属性:  

- table的属性
  - width="300px"   表格的宽度
  - height="300px"  表格的高度
  - border="1px"    表格的边框
  - align="left/center/right"   表格的水平对齐方式
  - bordercolor="red" 边框颜色
  - bgcolor="yellow"  背景颜色
  - cellpadding 单元格内边距，内容到边框的距离
  - cellspacing  单元格的外边距，边框与边框的距离

- tr的属性
  - bgcolor="yellow"  背景颜色
  - align="right"  **表格这一行的内容水平对齐方式**
  - valign  **表格这一行的内容垂直对齐方式**  
      取值  top/middle/bottom
- td的属性
  - width="200px"  
  - height="200px"  
  - align="right"   内容的水平对齐方式
  - valign="bottom" 内容的垂直对齐方式
  - bgcolor="red"
  - colspan  跨列
  - rowspan  跨行

### 不规则的表格

- 跨列：colspan  
从指定单元格位置处开始，横向向右合并n个单元格(n包括自己)，被合并的单元格要删除
- 跨行  
从指定单元格位置处开始，纵向向下合并n个单元格(n包含自己)，被合并的单元格要删除
- 可选标记  
  - 表格的标题  
\<caption>\</caption>  
如果要设置标题，caption必须放在\<table>之后  
  - 行/列的标题  
\<th>\</th>,td的属性，th都可以用  
**th的特点：文字加粗，水平居中**。  

### 表格的复杂应用  

我们制作的表格，浏览器解析的时候会自动添加上\<tbody>\</tbody>标签  

- 行分组：  
可以将连续的几行，划分到同一个组中，进行统一的管理。
  - 表头\<thead> \</thead>
  - 表主体\<tbody> \</tbody>
  - 表脚\<tfoot> \</tfoot>

- 表格的嵌套  
表格中所有的嵌套，都只能放在td中完成。  

---

## 列表（重点*******）

- 列表的作用  
按照从上到下，或者从左到右来显示所有的数据  
并且可以在数据前增加标识  

- 列表的组成  
列表都是由**列表类型**和**列表项**来组成的  
  1. 列表类型  
  有序列表 \<ol>\</ol> ==> order list  
  无序列表 \<ul>\</ul> ==> unorder list  
  2. 列表项  
  \<li>\</li>   list item  

1. 有序列表  
\<ol>  
 &nbsp; &nbsp; \<li>\</li>  
 &nbsp; &nbsp; \<li>\</li>  
 &nbsp; &nbsp; \...  
\</ol>  
属性：type  指定标识项的类型  
取值:  
  - 1 默认值，数字
  - a/A 字母
  - i/I 罗马数字

1. 无序列表---经常用于页面布局  
多个li的样式大体一致的时候，使用ul>li布局  
\<ul>  
 &nbsp; &nbsp; \<li>\</li>  
 &nbsp; &nbsp; \<li>\</li>  
 &nbsp; &nbsp; \...  
\</ul>  
属性：type 设置列表标识类型  
取值:  
  - .disc 默认值 实心圆
  - .circle 空心圆
  - .square 实心方块
  - .none  不显示

1. 列表的嵌套
原则，嵌套只能写在li中。不管是ol还是ul，直接子元素只能是li

1. 定义列表
h5新出的，一个名词，以及对这个名词的解释和定义  

```html
<dl>  定义列表
  <dt> </dt>  要解释说明的名词
  <dd> </dd>  对名词解释的内容
</dl>
```

## 结构标签

h5新出的标签，专门用于网页布局  
为了让代码有可读性，h5推出一堆与div功能一模一样的标签，专门用作网页布局  

- \<header>\</header>
定义网页的头部，或者某个区域的顶部
- \<footer>\</footer>
定义网页的脚部，或者某个区域的底部
- \<nav>\</nav>
定义网页的导航栏
- \<section>\</section>
定义网页的主体内容
- \<aside>\</aside>
定义网页的侧边栏
- \<article>\</article>
定义与文字相关的内容
比如，论坛，回帖，用户评论....

## 表单\*\*\*\*重点\*\*\*\*\*  

- 作用  
提供可视化的输入控件  
收集用户输入的信息，并提交请求给服务器  
总结：form自带提交请求的功能  
      ajax提交不需要form的支持  
      在同一个功能中，使用form就不用ajax,使用ajax就不用form  
- form的组成  
前端部分:提供表单控件，与用户交互的可视化控件  
后端部分:后台接口对提交的数据进行处理 nodejs+mysql  

### form表单详解

\<form>\</form>  
属性：  

- action="" 定义表单提交时，发送请求的动作(url)  
**如果不写值，默认提交给本页**  
- method="" 定义表单的提交方法  
取值  
  - get(默认值)  
特点：明文提交(参数在地址栏中显示)，不安全  
      提交的数据有大小限制，最大为2kb  
使用场合：向服务器要数据的时候，使用get  
  - post  
特点：隐式提交，参数不在地址栏中显示  
      提交数据没有大小限制  
使用场合：要传递数据给服务器的时候，使用post  
  - 其它的提交方法  
delete put option.......  

- enctype="" 指定表单数据的编码方式  
设置允许将什么类型的属性传递给服务器  
取值：  
  - application/x-www-form-urlencoded
默认值，允许将任意的字符提交给服务器
(不能提交文件)
  - text/plain 允许提交普通字符给服务器，不能包含特殊符号
  - multipart/form-data 允许提交文件给服务器  

\<form action="url" method="get"enctype="applicationx-www-form-urlencoded">\</form>:
收集的数据，发送给url这个接口，使用get提交  
要求提交的数据是任意字符，不是文件  

**表单控件**  
在form标签中，能够与用户交互的可视化控件  

**表单控件的分类:**  
input元素  基础9种  
textarea 多行文本域  
select+option下拉选择器  
其它元素  
h5新出的input元素 10种  

- input元素  
\<input type="">  
在页面中，input提供了各式各样的输入控件  
文本框，密码框，单选框，多选等....  
共同的属性  
  - type="" 指定input元素的类型
  - name="" **为控件定义名称，此名称是给服务器用的，如果想往服务器传递参数，此名称必须写**
  - value 是控件的值，真正传给服务器的值  
例外,**在按钮控件中,value是设置按钮上显示的文字**  
  - disabled 禁用，**不能修改值，也不能提交**  
      取值：  
    - disabled="disabled"  
    - disabled="true"  --js使用  
    - disabled  
            这种属性，称之为无值属性  

- **input详解9种**  

  - (2) 文本框和密码框  
文本框 type="text"  input默认是text  
密码框 type="password"  
属性：  
maxlength 设置输入的最大值  
readonly 无值属性，**不能修改，允许提交**  
placeholder 占位提示符  
  - (3)按钮  
提交按钮 type="submit"  
    将表单中的数据收集整理，发送给服务器  
普通按钮 type="button"  
    没有功能，配合事件，调用js代码  
重置按钮 type="reset"  
    将当前表单内容恢复到初始化状态  
按钮中value，设置按钮上的文本，此value不提交  
关于按钮的题外话  
h5给我们推出了新的按钮标签:  
**\<button>\</button> 自带submit功能**  
  - (2)单选和复选按钮  
单选按钮 type="radio"  
多选按钮 type="checkbox"  
属性name，除了定义控件名称之外，还起到分组的作用，分了组才会有单选效果  
**必须有value属性，不然传递的参数永远是on**  
checked 无值属性 设置默认被选中的项  
  - (1)隐藏域  
type="hidden"  
想把数据提交给服务器，但是又不想用户看到  
这种数据放到隐藏域中  
用户看不见，但是可以提交  
  - (1)文件选择框，上传文件  
type="file"  
前提：提交方法，使用post  
      enctype属性，设置为multipart/form-data  
**属性multiple，可以选择多个文件上传**  
- **h5新表单元素**
  - 邮箱，提交的时候，验证@以及@前后至少有一个字符  
\<input type="email">  
  - 搜索类型，自带快速清除功能  
\<input type="search">  
  - url类型，提交时，验证以http://开头  
\<input type="url">
  - 电话号码，移动端使用时，会弹出虚拟键盘  
\<input type="tel">  
  - 数字类型  
\<input type="number" max="10" min="2" step="3">  
max：能接收的最大值  
min：能接收的最小值  
step：步长，按一次按钮，变化几个数字  
  - 范围类型  
\<input type="range" max="22" min="10" step="4">  
max：能接收的最大值  
min：能接收的最小值  
step：步长，按一次按钮，变化几个数字  
  - 颜色类型  
\<input type="color">  
  - 日期类型，提供了一个日期选择的控件  
\<input type="date">  
  - 月份类型  
\<input type="month">  
  - 周类型  
\<input type="week">  
  - \<button>\</button>  
替代\<input type="submit"> 有提交功能 增加可读性  
- textarea多行文本域  
\<textarea>\</textarea>  
允许录入多行文字  
cols 设置输入的列数  
rows 设置输入的行数  
根据计算硬件不同，不准确  
- 下拉选  
\<select>  
  \<option>\</option>  
  \<option>\</option>  
  ....  
\</select>  
注意：  
1.**如果option没有value，那么select的value是option的内容**  
2.**如果option有value,那么select的value是选中option的value值**  
属性 name  value  
selected  默认选中  
size 默认值为1，  
     值为1的时候，为下拉选择框  
     值>1的时候，为滚动选择框  
multiple 无值属性，多选  
- 其它元素  
label 关联文本与表单的控件  
\<label for="">\</label>
属性for绑定要关联的表单控件的ID
- 为控件分组  

```html
<fieldset> 分组  
  <legend>标题</legend>  
  form表单控件...  
</fieldset>  
```

## 浮动框架

\<iframe style="width:100%" src="01_ex.html"
frameborder="0" scrolling="no">\</iframe>  
语法: \<iframe>\</iframe>  
属性:  
    src 引用的资源路径  
    frameborder="0" 清除边框  
    scrolling="no" 清除滚动条  
    width/height  
