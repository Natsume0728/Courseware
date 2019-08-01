# CSS

<!-- TOC depthFrom:2 orderedList:false -->

- [CSS概述](#css概述)
- [css的语法规范](#css的语法规范)
- [基础选择器(重点！！！！！！)](#基础选择器重点)
    - [选择器详解](#选择器详解)
    - [选择器的权值](#选择器的权值)
- [尺寸和边框](#尺寸和边框)
    - [尺寸属性](#尺寸属性)
    - [页面中允许设置尺寸的元素](#页面中允许设置尺寸的元素)
    - [溢出处理](#溢出处理)
    - [边框](#边框)
        - [边框属性](#边框属性)
        - [单边定义边框](#单边定义边框)
        - [单属性定义](#单属性定义)
        - [单边单属性](#单边单属性)
    - [边框的倒角(圆角)](#边框的倒角圆角)
    - [边框阴影](#边框阴影)
    - [轮廓](#轮廓)
- [框模型---盒子模型](#框模型---盒子模型)
    - [外边距margin](#外边距margin)
        - [语法](#语法)
        - [外边距的特殊效果](#外边距的特殊效果)
        - [关于块级元素，行内元素，行内块的外边距总结](#关于块级元素行内元素行内块的外边距总结)
        - [自带外边距的元素](#自带外边距的元素)
        - [外边距溢出](#外边距溢出)
    - [内边距](#内边距)
    - [box-sizing属性(设置元素实际占地尺寸的公式)](#box-sizing属性设置元素实际占地尺寸的公式)
- [背景](#背景)
- [渐变 gradient](#渐变-gradient)
- [文本格式化(重点********)](#文本格式化重点)
    - [字体属性](#字体属性)
    - [文本属性](#文本属性)
- [表格的样式](#表格的样式)
    - [表格的常用样式属性table>tr>td](#表格的常用样式属性tabletrtd)
    - [表格特有的样式属性](#表格特有的样式属性)
        - [自动布局与固定布局](#自动布局与固定布局)
- [定位(重点**************************)](#定位重点)
    - [定位的分类](#定位的分类)
    - [普通流定位](#普通流定位)
    - [浮动定位](#浮动定位)
        - [浮动定位引发的特殊情况](#浮动定位引发的特殊情况)
        - [清除浮动](#清除浮动)
        - [高度坍塌](#高度坍塌)
- [定位---相对，绝对，固定定位（**************************）](#定位---相对绝对固定定位)
    - [position](#position)
    - [堆叠顺序](#堆叠顺序)
- [元素的显示方式](#元素的显示方式)
    - [display](#display)
- [显示效果](#显示效果)
    - [visibility](#visibility)
- [透明度](#透明度)
    - [opacity](#opacity)
- [垂直对齐方式](#垂直对齐方式)
    - [vertical-align](#vertical-align)
- [光标的设置](#光标的设置)
    - [cursor](#cursor)
- [列表的样式](#列表的样式)
    - [ul的样式](#ul的样式)
- [CSS3 CORE](#css3-core)
    - [复杂选择器](#复杂选择器)
        - [兄弟选择器](#兄弟选择器)
        - [属性选择器](#属性选择器)
        - [伪类选择器](#伪类选择器)
        - [伪元素选择器](#伪元素选择器)
            - [伪元素内容添加，可以解决的问题](#伪元素内容添加可以解决的问题)
- [弹性布局（重点*******************************************）](#弹性布局重点)
    - [弹性布局相关的概念和名词解释](#弹性布局相关的概念和名词解释)
    - [弹性布局语法](#弹性布局语法)
- [CSS hack](#css-hack)
- [转换（重点**************************）](#转换重点)
    - [转换的属性](#转换的属性)
        - [transform](#transform)
        - [转换原点](#转换原点)
        - [2D转换](#2d转换)
        - [3D转换---3d都是模拟](#3d转换---3d都是模拟)
            - [透视距离 perspective](#透视距离-perspective)
            - [3D旋转](#3d旋转)
- [过渡（重点*****************）](#过渡重点)
    - [过渡语法](#过渡语法)
        - [指定过渡的属性](#指定过渡的属性)
        - [指定过渡时长](#指定过渡时长)
        - [过渡时间曲线函数](#过渡时间曲线函数)
        - [过渡的延迟时间](#过渡的延迟时间)
        - [过渡代码的编写位置](#过渡代码的编写位置)
        - [简写方式](#简写方式)
- [动画](#动画)
    - [使用关键帧来控制动画的每一个状态](#使用关键帧来控制动画的每一个状态)
    - [使用动画](#使用动画)
    - [动画的兼容性](#动画的兼容性)
- [CSS优化](#css优化)
- [响应式布局(css3)](#响应式布局css3)
    - [响应式网页必须保证几件事情](#响应式网页必须保证几件事情)
    - [如何测试响应式网页](#如何测试响应式网页)
    - [编写响应式布局(重点**************************)](#编写响应式布局重点)

<!-- /TOC -->

## CSS概述

1. 什么是css
Cascading style sheets 层叠样式表，级联样式表
简称样式表
1. css的作用  
设置html网页中元素的样式，美化页面
1. HTML与CSS的关系  
HTML：负责网页的搭建，内容的展示  
CSS：负责网页的修饰，样式的构建  
![CSS_001.jpg](https://i.loli.net/2019/06/28/5d14ede93771894587.jpg)
1. CSS与HTML的属性，使用原则  
W3C规定我们尽量的使用css的方式来取代HTML属性
css样式
   - 样式代码可以高度重用，html属性不能重用
   - 方便后期维护，提高可维护性。

## css的语法规范

1. 使用css样式的方式
   - 行内样式(内联样式)  
在html标签的style属性中，编写样式  
语法：\<any style="样式声明">\</any>  
样式声明："样式属性 : 值"  
有多个样式声明："样式属性1：值1 ；样式属性2：值2"  
ex:  
`<div style="color:red;background-color:yellow">`  
内联样式在项目中，很少使用,学习和测试的时候用。  
原因：  
     1. **内联样式不能重用**  
     2. **内联样式优先级最高**  
   - 内部样式  
在网页头部中，添加一对\<style>\</style>标签  
在style标签中定义此网页所有的样式:  
\<style>  
   选择器{样式属性：值；样式属性：值；........}  
\</style>  
选择器：就是一个条件，符合这个条件元素，可以应用这个样式  
项目中使用内部样式较少，学习和测试使用较多。  
内部样式的重用不能在其他html页面中生效  
   - 外部样式  
单独创建一个css文件，编写样式  
在html页面的head中使用link，引入这个外部样式  
`<link rel="stylesheet" href="css文件的url">`  
注意：**rel="stylesheet"必须写，不然无效;**  
此种方式，是开发中使用最多方式。  
1. CSS的特性
   1. 继承性  
**大部分(宽，高,尺寸，边框，定位等不会被继承，a标签的字体颜色不会继承)的css效果，是可以被子元素继承的;**  
**必须是父子结构，子继承父;**  
   1. 层叠性  
**可以为一个元素定义多个样式规则;**  
**多个规则中样式属性不冲突时**，可以同时应用到当前元素上;  
   1. 优先级  
如果对一个元素的多个样式声明，发生冲突时，按照样式规则的优先级去应用;  
默认优先级：由高到低(不考虑继承的样式)  
       1. 内联样式(行内样式)  
       2. 内部样式和外部样式，就近原则
       3. 浏览器默认样式
   1. 调整优先级  
!important规则  
放在属性值后面，与值之间有一个空格;  
作用，调整样式显示的优先级;  
**内联样式不可以写!important** ;  
!important优先级，比内联样式高;  

## 基础选择器(重点！！！！！！)

>选择器的作用:  
规范了页面中哪些元素能够使用定义好的样式,  
选择器就是为了匹配元素用,  
(选择器是一个条件，符合这个条件的元素就可以使用这个样式)  

### 选择器详解

1.  **通用选择器**  
*{样式声明}  
由于*的效率低下，项目中很少使用通用选择器;  
唯一使用的场合:`*{margin:0;padding:0}`所有元素内外边距清零；  
02. **元素选择器(标签选择器)**  
页面中所有对应的元素，都应用这个样式；  
设置页面中某种元素的默认样式；  
元素名称{样式声明}  
ex:p{}   div{}
03. **ID选择器，专属定制**  
\<any id="id值">\</any>  
\#id值{样式声明}  
这种写法仅仅对页面上一个标签生效;  
一般id选择器在项目中很少单独使用。  
通常会作为子代选择器或者后代选择器的一部分。  
04. **类选择器**  
\<any class="类名">\</any>  
.类名{样式声明}  
作用：定义页面上某个或者某类元素的样式  
(公共样式，谁想用，谁就可以用)  
class属性来引用类名  
类名的规则：  
    - 类名之前的点不能省略，引用的时候没有点
    - 类名不能以数字开头
    - 类名只能包含 -  _ 符号
    - 类名尽量的见名知意  
**类选择器的特殊用法:**  
     1. 多类选择器  
让元素引用多个类名，这些类的样式都会作用到当前元素上  
`<div class="text-danger bg-warning font-24">some thing</div>`  
     1. 分类选择器(**只有如下两种情况可以使用,与其它如id选择器等不能混用**)  
        - 元素选择器+类选择器{}  
div.text-danger{ }  
div元素有text-danger类,才能应用这个样式  
        - 类选择器+类选择器{}  
.font-24.text-danger{ }  
元素，必须有font-24类和text-danger，才能应用此样式  
作用：  
1.更精确的确定使用样式的元素  
      2.增加选择器的权值  

05. **群组选择器**  
将多个选择器放在一起定义公共的样式  
语法：选择器1,选择器2,......{公共样式声明}  
ex:  
`#content,div,.mycolor,p.text{color:red}`  
相当于  
`#content{color:red}`  
`div {color:red}`  
`p.text {color:red}`  
`.mycolor {color:red}`  
06. **后代选择器**  
通过元素的后代关系匹配元素  
后代：一级嵌套或者多级嵌套  
语法：选择器1  选择器2  选择器3........{}  
`#content p span{color:red;}`  
id为content的元素，内部不管隔着多少代，有一个p元素  
p元素内部，不管隔着多少代，有一个span，这个span就符合要求  
07. **子代选择器**  
通过元素的子代关系匹配元素  
子代：一级嵌套，直接的儿子  
选择器1>选择器2>....{}  
子代选择器和后代选择器可以混写  
`#content p>span{background-color:yellow;}`  
08. **伪类选择器**  
匹配同一个元素，不同的状态下的样式  
所有的伪类选择器都是这样开头的: **选择器：**  
**多个伪类选择器作用在同一个元素上时，必须按照一定的顺序编写，否则会冲突：爱恨原则 "love hate"**;  
     - 链接伪类  
       - a标签，没有访问的状态===> a:link{color:red;}  
       - a标签，被访问过之后的状态===> a:visited{color:black;}  
     - 动态伪类  
       - :hover 鼠标悬停在元素上时，元素的样式
       - :active 匹配元素被激活时的状态(如:a标签被按下未抬起)
       - :focus 匹配元素获取焦点时的状态  

### 选择器的权值

权值：标识当前选择器的重要程度，权值越大，优先级越高  

- !important   >1000  
- 内联样式     1000  
- id选择器     100  
- 类选择器      10  
- 元素选择器     1  
- *通用选择器    0  
- 继承的样式    无  

权值的特点  

1. 当一个选择器中含有多个选择器时，需要将所有的选择器权值进行相加，然后比较，权值大的优先显示;  
2. 权值相同，就近原则;  
3. **群组选择器的权值，单独各算各的，不能相加**;  
4. 样式后面追加!important直接获取最高优先级;  
  内联样式不能加!important  
5. 选择器的权值计算，结果不会超过自己的最大**数量级**;  
(1000个1相加，也不会大于10)

## 尺寸和边框

### 尺寸属性

作用，设置元素的宽高  
属性：  
width: 设置宽  
height:设置高  
max-width 最大宽度  
min-width 最小宽度  
max-height 最大高度  
min-height 最小高度  
使用场合：**响应式布局**  

取值：  
以px为单位的数字  
      父元素尺寸的%百分比  
>附加知识点：单位  
尺寸的单位  

- px像素  
- in英寸  1in=2.54cm  
- pt 磅值，多用于修饰字体大小粗细  1pt=1/72in
- cm
- mm
- % 父元素的百分之多少
- em 是相对于父元素数值的单位
- rem 是相对html标签数值的单位

### 页面中允许设置尺寸的元素

- 块级元素  
所有的块级元素都可以设置尺寸  
**块级元素不设置宽，宽度占父元素100%。**  
**块级元素不设置高，高度靠内容撑开，没有内容，就没有高。**  
- 行内元素  
**行内元素设置宽高无效，**  
**行内元素宽高，是靠内容撑开**  
**但是，自带宽高属性的行内元素(如 img)，可以设置尺寸**  
- table  
table自带宽高属性，可以设置宽高  
- 行内块  
input  
行内块可以设置宽高  

### 溢出处理

当内容较大，元素区域较小，就会发生溢出效果；  
默认是纵向溢出  
属性 overflow  
取值  

   1. visible 默认值，溢出部分可见
   2. hidden 溢出部分隐藏
   3. scroll，不管是否溢出，都添加滚动条。  
              不溢出的时候，滚动条不能拖动  
   4. auto 自动，溢出的时候，溢出的方向有滚动条。  
            不溢出的时候，没有；  
控制滚动条的方向：  
     overflow-x/overflow-y  
**如何让内容横向溢出**  
  需要在宽度比较小的容器内部，添加一个宽度较大的元素盛放内容，  
  在父容器上写overflow:auto。就可以做到横向溢出。  

**附加知识点---颜色**  
合法颜色值  

1. 颜色的英文单词(red,blue,yellow,pink,purple......)
2. #rrggbb  
   #000000---黑  
   #ffffff---白  
   #ff0000---红  
   #00ff00---绿  
   #0000ff---蓝  
3. #aabbcc---->#abc  
   #000 #fff  #f00  #0f0  #00f  #666  
4. rgb(0~255,0~255,0~255)  
  rgb(255,0,0)  
5. rgba(r,g,b,alpha)  
alpha透明度: 0~1 , 1不透明，0透明  

>\#f00 #0f0 #00f  #ff0 #0ff #f0f  
\#faa #afa #aaf  #ffa #aff #faf  

### 边框

#### 边框属性

简写方式---4个方向边框一起设置  
border:width style color;  

- width:边框的宽度，取值以px为单位的数字  

- style:边框的样式 取值：  

  - solid实线  
  - dotted 点点虚线  
  - dashed 线状虚线  
  - double 双实线  

- color：边框的颜色  
取值 合法的颜色值/transparent(透明)  
最简方式 border:style;  
取消边框 border:0;  或者 border:none;  

#### 单边定义边框

只设置某一条边的3个属性  
border-top：width style color;  
border-right  
border-bottom  
border-left  

#### 单属性定义

border-width:  
border-style:  
border-color:  
ex:  
border-width:3px;  
border-style:solid;  
border-color:#f00;  
border:3px solid #f00;  

#### 单边单属性

border-top-width:  
border-top-style:  
border-top-color:  

border-right-width:  
border-right-style:  
border-right-color:  

border-bottom-width:  
border-bottom-style:  
border-bottom-color:  

border-left-width:  
border-left-style:  
border-left-color:  

### 边框的倒角(圆角)

将直角设置成倒角，圆角  
border-radius：  
取值：  

- 以px为单位数字
- %  
50%就是个圆  

单角设置  
border-top-left-radius  
border-top-right-radius  
border-bottom-left-radius  
border-bottom-right-radius  

### 边框阴影

**box-shadow**  
取值：[h-shadow] [v-shadow] [blur] [spread] [color]  [inset];  

- h-shadow:水平方向的阴影偏移量  
      +：往右移动， -：往左移动  
- v-shadow:垂直方向的阴影偏移量  
      +：往下       -：往上  
- blur：阴影模糊距离，越大越模糊  
      无负值  
- spread：阴影尺寸，在基础阴影上扩出来的大小  
      负值，尺寸变小  
- color:阴影颜色  
- inset:向内扩撒阴影  

### 轮廓

轮廓指的是边框的边框，绘制于边框外的线条  
outline:width style color;  
outline:none;或者outline:0 去除轮廓  

## 框模型---盒子模型

框模型--元素在页面上实际占地空间的计算方式  
>默认情况，  
一个元素在页面的实际占地宽度:  
左外边距+左边框宽度+左内边距+内容区域宽度+右内边距+右边框+右外边距;  
实际占地高度:  
上外边距+上边框宽度+上内边距+内容区域高度+下内边距+下边框+下外边距;  

### 外边距margin

元素边框以外的距离，改变margin，元素有位移的效果  

#### 语法

- margin:v1;  
 设置4个方向的外边距  
- margin:v1 v2;  
v1上下   v2左右  
  - margin:0 auto; 块级元素水平居中  
           auto对垂直外边距无效  
  - margin:auto;  
           auto只对设置了宽的块级元素生效  
- margin:v1 v2 v3;  v1上  v2左右  v3下
- maring:v1 v2 v3 v4;  上右下左  

单方向外边距设置  
margin-top:  
margin-right:  
margin-bottom:  
margin-left:  

取值：  

- 以px为单位数字
- %
- \+ margin-top ↓   margin-left →  
        - margin-top ↑   margin-left ←
- auto  
自动计算块级元素外边距，让块级元素水平居中  
             auto只对设置了宽度的块级生效  
             auto对下上外边距无效  

#### 外边距的特殊效果  

- **外边距合并**

两个垂直外边距相遇时，他们将合并成一个，值以大的为准,  
只能在布局设计的时候，尽量避免发生  

#### 关于块级元素，行内元素，行内块的外边距总结

- 行内元素的特点：  
设置宽高无效，宽高根据内容自动撑开  
上下垂直外边距无效。可以与其他的行内元素和行内块元素共用一行  
- 块级元素特点：  
设置宽高有效。  
如果不设置宽高，高按内容撑开，宽占父元素宽度的100%。  
上下外边距有效，独占一行.
- 行内块的特点：input  
设置宽高有效，不设置宽高，自带默认宽高。  
上下外边距有效，但是同一行修改一个行内块的垂直外边距，整行都会跟着一起改变位置。  
可以与其他行内元素和行内块共用一行。  

#### 自带外边距的元素  

body h1~h6 p ol ul dl pre  
由于不同浏览器对默认的外边距解析可能有差别  
所以一般情况下，开发之前，需要把内外边距清空  
\*{margin:0;padding:0}  
或者通过群组选择器来写  
blockquote,body,button,dd,dl,dt,fieldset,form,
h1,h2,h3,h4,h5,h6,hr,input,legend,li,ol,
p,pre,td,textarea,th,ul{margin:0;padding:0}  

#### 外边距溢出

在特殊情况下，为子元素设置外边距，会作用到父元素上  
特殊情况：  
1.父元素没有上边框  
2.子元素内容区域上边与父元素内容区域上边重合的时候  
(为父元素中第一个子元素设置上外边距时，这种说法不严谨)  
解决方案：  
1.给父元素添加上边框，弊端，影响父元素实际占地高度  
2.给父元素添加上内边距，弊端，影响父元素实际占地高度  
3.**给父元素的一个子元素的位置添加空table元素**  

### 内边距

内边距的改变效果，感觉是改变了元素的大小  
不会影响其它元素，但是真正改变的是本元素的占地尺寸  
**内边距颜色和元素背景相同**  

语法：  

- padding:v1;  
设置4个方向的内边距
- padding:v1 v2;  
上下   左右  
padding无auto  
- padding:v1 v2 v3;  
 上  左右  下
- padding:v1 v2 v3 v4;  
上右下左

单方向设置  

- padding-top
- padding-right
- padding-bottom
- padding-left

取值  

- 以px为单位的数字  
- %  

**padding无auto值**!

### box-sizing属性(设置元素实际占地尺寸的公式)

box-sizing:  
取值：  

- content-box  
默认值，按照之前的盒子模型计算元素占地大小  
(左外+左边+左内+内容区域宽度+右内+右边+右外)
- border-box  
设置的width和height是包含border+padding+内容区域的整体宽高  
      元素实际占地大小：  
      左外+设置的width+右外  
      上外+设置的height+下外  
给复杂元素关系做布局时，经常使用border-box  

## 背景

1. 背景颜色  
background-color:合法颜色值  
2. 背景图片  
background-image:url(08.png);  
使用背景图片，可以让该元素的子元素，堆叠显示在背景图片上。  
而使用img标签，默认不会有堆叠效果  
3. 背景图片的平铺  
background-repeat:  
取值：  
   - repeat 默认值，平铺
   - no-repeat 不平铺
   - repeat-x   水平方向平铺
   - repeat-y   垂直方向平铺
4. 背景图片的定位  
background-position:  
取值：  
   - x  y  以px为单位的数字
   - x% y% 百分比
   - 关键字  
   x:left/center/right  
                y:top/center/bottom
5. 背景图片的尺寸  
background-size:  
取值：  
   - x  y  
   以px为单位设置具体宽高
   - x% y%  
   按父元素宽高比设置，以元素的角度考虑这两个单词
   - cover  
   充满，只要求元素被背景图充满，背景图显示不全，也没关系.
   - contain  
   包含，只要求元素要把背景图整个包含住，元素有空白，也没关系
6. 背景图片的固定  
background-attachment  
取值：  
   - scroll  
   默认值，背景图会随着窗口滚动条滚动
   - fixed  
   固定，背景图相对于窗口固定，窗口滚动时，背景图位置不变，但是只会在原容器内显示
7. 背景的简写方式  
background:  
取值  [color][image] [repeat] [attachment] [position]  
最精简方式 background:color/image;

## 渐变 gradient

1. 什么是渐变  
渐变是指多种颜色，平缓变化的一种显示效果  
2. 渐变的主要因素  
色标：一种颜色，以及这种颜色出现的位置  
一个渐变，最少两个色标
3. 渐变的分类  
    1. 线性渐变，以直线的方式，来填充渐变色
    2. 径向渐变，以圆形的方式，来填充渐变色
    3. 重复渐变，将线性，径向渐变重复几次显示
    - 线性渐变  
background-image:  
linear-gradient(angle,color-point1, color-point2......);  
        - angle:表示渐变的方向  
     取值  
     1.关键字  
     to top    从下往上  
                   to right   从左往右  
                   to bottom 从上往下  
                   to left     从右往左  
           2.角度  
           0deg  to top  
                   90deg to right  
                  180deg to bottom  
                  270deg to left  
                  可以取负值  
        - color-point:色标  颜色 %/px
    - 径向渐变
background-image:  
radial-gradient(半径 at 圆心x 圆心y,color-point1,color-point2.................)  
        - 半径 以px为单位的数字
        - 圆心  
            1. x  y  以px为单位的数字
            2. x% y%
            3. 关键字  x left/center/right  
                y top/center/bottom
        - color-point: 位置取值  
            1. %   半径的百分比%  
            2. **px为单位的数字，半径失效**
    - 重复渐变  
重复的线性渐变  
background-image:  
repeating-linear-gradient(to left,#000 0px,#ff0 25px,#000 50px);  
重复的径向渐变  
background-image:  
repeating-radial-gradient(50px at center center,\#000 0%,#0ff 25%,#000 50%);  
4. 浏览器兼容问题  
如果有低版本(ie8.0以下)，想要使用渐变  
chrome/safari  -webkit-  
firefox         -moz-  
opera          -o-  
IE              -ms-  
要低版本兼容渐变，需要在linear-gradient之前添加浏览器内核  
background-image:  
-webkit-linear-gradient()  
background-image:  
-moz-linear-gradient()  
......  
兼容低版本浏览器，线性渐变的方向，要改变写法  
不写to top/to left/to bottom/to right  
改成初始点 top/left/bottom/right  

## 文本格式化(重点********)

### 字体属性

1. 字号大小  
font-size:  
取值：px/pt/em/rem  
2. 设置字体类型  
font-family:"mv boli",华文彩云,黑体;  
在当前设备的字体库，查找字体，如果有就使用，如果没有，就查找下一个。  
如果字体名称中间有空格，必须加双引号  
3. 粗体  
font-weight:  
取值  
    1. 关键字 lighter  normal  bold  bolder  
    2. 无单位的100的整倍数  一般400~1000
4. 字体样式  
font-style:normal/italic;  
正常和斜体
5. 小型大写字母  
font-variant:small-caps;  
6. 简写方式  
font:style variant weight size family;  
font:italic small-caps bolder 40px chiller;  
最精简的方式 font:size family;  

### 文本属性  

1. 字体颜色  
color  
2. 文本水平对齐方式  
text-align:  
取值  
left/center/right/justify两端对齐  
margin:0 auto和text-align:center的区别:  
margin:0 auto，控制的是当前元素本身在页面中居中(让自己居中)  
text-align:center 控制的是当前元素内部的内容，在元素内部居中(让我的儿子居中)  
3. 行高  
定义一行数据的高度  
特性：  
如果行高的高度大于字体本身的大小  
      那么该行文本将在指定的行高内，呈垂直居中方式显示  
line-height  
取值：  
    1. 以px为单位的数字，  
    一般，行高的值与容器高度相同。  
        这样就可以让文字在容器垂直中间显示了。  
    2. 无单位的数字(整数小数都可以)，行高为字号大小的倍数  
注意:**文字如果有多行，不建议使用行高，文字会溢出，每一行的行高都是你设置的大小**  
4. 文本线条修饰  
text-decoration  
取值：  
    - overline 上划线
    - underline 下划线
    - line-through 删除线
    - none 去掉所有的修饰线条  
      a{text-decoration:none}去除a标签下划线
5. 首行缩进  
text-indent:  
取值：  
px为单位的数字  
6. 文本阴影  
text-shadow:h-shadow v-shadow blur color;  
    - h-shadow:水平偏移
    - v-shadow:垂直偏移
    - blur：阴影模糊度
    - color：阴影颜色

## 表格的样式

### 表格的常用样式属性table>tr>td  

- table:之前学习过的样式，基本都可以使用  
尺寸，边框，背景，字体，文本，内外边距  
给table设置border,只设置最外面的大边框  
- td/th的样式  
尺寸，边框，背景，字体，文本，内边距  
外边距无效  
vertical-align指定单元格数据的垂直对齐方式  
取值：  
top/middle/bottom  

>表格是一种特殊的表现方式  
表格实际尺寸是根据内容数据的多少而决定的
单元格小，内容多，自动撑开
内容少，单元格就按照设置的尺寸来展示

### 表格特有的样式属性  

- 边框合并  
border-collapse:  
取值 ：  
  - separate 默认值，边框分离模式
  - collapse;边框合并模式  
- 边框边距  
向设置边框边距，必须保证边框是分离状态  
border-collapse:separate ;  
属性border-spacing:  
取值：  
  - 只有一个值  
         设置水平和垂直边框的 外边距
  - 两个值  
        第一个值设置水平  第二个值设置垂直  
- 标题位置  
caption-side:  
取值：  
  - top 默认值
  - bottom  
- 设置表格的显示规则：用来确定如何布局一张表格  
table-layout  
取值  
  - auto 默认值  
        自动布局表格  
            列的尺寸实际使用内容决定的，内容比尺寸大，按照
            内容大小显示。  
            内容比尺寸小，按照尺寸显示
  - fixed  
        固定表格布局，列的尺寸以设置的为准

#### 自动布局与固定布局

|自动布局|固定布局|
|:---:|:---:|
|单元格的大小自动适应内容|单元格大小取决于设置的值|
|表格复杂时，加载速度较慢|任何情况下，都会加速加载表格(优点)|
|比较灵活(优点)|固定布局不够灵活|
|适用于不确定每列大小的，并且不复杂的表格|适用于能够确定每列尺寸大小的表格|

## 定位(重点**************************)

>什么是定位  
改变元素在页面中的位置  

### 定位的分类

1. 普通流定位
2. 浮动定位
3. 相对定位
4. 绝对定位
5. 固定定位

### 普通流定位

又称为默认文档流定位  

1. 每个元素在页面上都有自己的空间
2. 每个元素都是从父元素的左上角开始渲染（显示）
3. 块级元素按照从上到下逐个排列，每个元素单独成行
4. 行内元素是多个元素在一行中显示，从左往右顺序排列，显示不下换行

### 浮动定位

>让块级元素横向显示  

float 取值：  

- left  
让元素浮动后，在当前行停靠在父元素的左侧，或者挨着左侧已浮动元素
- right  
让元素浮动后，在当前行停靠在父元素的右侧，或者挨着右侧已浮动元素
- none  
默认值，不浮动

浮动的特点  

1. 元素一旦浮动，脱离文档流(不占页面空间，后面未浮动元素会上前补位)
2. 浮动元素会在**当前行**，停靠在父元素的左/右边，或者停靠在其他已浮动元素的边缘
3. 当父元素横向显示不下所有浮动元素时，最后显示不下的，会自动换行
4. 浮动用于解决，多个块级元素在同一行显示的问题

#### 浮动定位引发的特殊情况

1. 浮动元素占位的问题  
 当元素显示不下所有浮动元素时，最后显示不下的元素会换行  
 但是，**已浮动元素会根据自己的浮动方向占据位置**，  
 导致被挤下去的浮动元素，需要让开位置，在更下面的地方显示  
 ![CSS_002.jpg](https://i.loli.net/2019/06/28/5d151d418ea9231460.jpg)
2. 元素一旦浮动，如果元素未定义宽度，那么元素浮动之后的宽度将以内容为准  
![CSS_003.jpg](https://i.loli.net/2019/06/28/5d151d417516967282.jpg)
3. 元素一旦浮动，都会变成块级元素  
  允许设置尺寸，可以设置垂直外边距
4. 文本，行内元素，是不会被浮动元素压在下面的,  
而是巧妙的避开，环绕着浮动元素显示

#### 清除浮动

清除之前的浮动元素给自己带来的影响  
由于元素浮动之后，会脱离文档流，会让后续不浮动的元素上前补位.  
如果后续元素不想上前补位，需要对此元素设置清除浮动  
clear:  
取值：  

- left  清除左浮动对我的影响
- right 清除右浮动对我的影响
- both 清除左右浮动对我的影响
- none 不清除影响

#### 高度坍塌

什么叫高度坍塌  

1. 父元素不写高，靠子元素撑起高度
2. 所有子元素都浮动
那么所有子元素都脱离文档流，父元素认为自己内部没有元素了  
所以父元素就没有高度了  

解决方案：  

1. 父元素也浮动，弊端，影响父元素后面的非浮动元素
2. 直接给父元素写高度 弊端，不是每次都能知道具体高是多少
3. overflow：hidden 弊端，会让真正要溢出不能显示
4. 在父元素中追加一个块级元素，  
这个块级元素，没有内容，不写高,只写clear:both,  
就可以让父元素在文档流中找到内容的高度,
解决高度坍塌问题。

## 定位---相对，绝对，固定定位（**************************）

### position

取值：  

- static 默认，静态(默认文档流定位)
- relative 相对定位
- absolute 绝对定位
- fixed    固定定位

>已定位元素:当一个元素，被position修饰，并且取值为relative/absolute/fixed其中一种时，这个元素被称为已定位元素;  
>>已定位元素，解锁了4个偏移属性,偏移属性，定义了元素距离某一个方向移动了多少距离;  

- top     + 往下  - 往上
- right    + 往左  -往右
- bottom + 往上  -往下
- left     +往右 -往左

1. 相对定位 position:relative;  
相对定位，相对自己原来位置偏移某个距离  
配合4个偏移属性使用  
特点：  
   - **不脱离文档流**。后面元素不会上前补位
   - 相对定位，如果不写偏移量，元素效果与没写定位是一样的.  
  
      使用场合：  
①自身位置的微调  
②**作为绝对定位的祖先级元素**  
1. 绝对定位 position:absolute；  
配合偏移量使用  
特点：  
①绝对定位，**脱离文档流(当前元素不写宽，靠内容撑起来)，元素不占页面空间，后面元素上前补位**。  
②绝对定位的元素，会相对于  
"**离自己最近的**""**已定位的**""**祖先元素**"实现位置的初始化  
  如果没有 "已定位的""祖先元素"，相对于body实现位置初始化  
③**绝对定位元素会变成块级元素**  
④绝对定位元素，如果不写宽，定义之后，宽靠内容撑开  
1. 固定定位 position:fixed;  
配合偏移量使用  
将元素固定在页面的某个位置，不会随着滚动条发生位移变化  
特点：  
   - 脱离文档流
   - 元素变为块级元素
   - 不写宽会被内容撑开
   - 相对body做位置的初始化

### 堆叠顺序

特点：  

- 默认堆叠顺序，后定位的元素，堆叠顺序高
- 定位的脱离文档流，和浮动的脱离文档流，不是一个体系
- 使用z-index设置堆叠顺序  
     z-index:无单位数字   一般情况 1~1000 理论情况可取值: 2<sup>16</sup>;
- 堆叠顺序，只对已定位元素有效
- 堆叠顺序，对父子级无效。子元素永远在父元素上面显示

## 元素的显示方式

### display

取值：  

- block 让元素的表现和块级一致
- inline  与行内元素一致
- inline-block 与行内块元素一致
- table 与table一致
- none  不显示元素，隐藏  

块级：独占一行，可以设置尺寸，上下外边距有效  
行内：共用一行，尺寸无效，上下外边距无效  
行内块：共用一行，可以设置尺寸，上下外边距有效  
table：独占一行，可以设置尺寸，尺寸以内容为主  

## 显示效果

### visibility

取值：  

- visible 默认值，可见
- hidden 隐藏不可见  

问题：**visibility:hidden和display:none区别**  
visibility:hidden:  
隐藏，元素不脱离文档流，在当前页面不可见，但是占据位置  
display:none:  
隐藏，元素脱离文档流，隐藏后不占位置，后面元素上前补位

## 透明度

### opacity

取值：0~1 值越小越透明  

问题：**opacity和rgba的区别**  
rgba只会改变当前颜色的透明度  
opacity，元素内部只要元素相关的颜色都会跟着透明  

## 垂直对齐方式

### vertical-align

使用场合  

- 表格中  td/th  
 取值: top/middle/bottom  
- img与文字的排版  
 **改变的是img与前后文本的对齐方式(不是改变img自己)**  
 取值: top/middle/bottom/baseline基线  
通常，会将所有的图片与文字的对齐方式，改为**非基线对齐**的方式

## 光标的设置

### cursor

取值：  

- default 箭头
- pointer 小手
- crosshair  十字
- text  文本输入的I
- wait 等待
- help 帮助

## 列表的样式

### ul的样式

- 列表项标识  
list-style-type:  
 取值 none/disc/circle/square  
- 列表项标识，设置为图片(图片要小)  
list-style-image:url(路径);  
- 列表项标识的位置  
list-style-position:inside/outside(默认值)  
设置列表项是在li的内部还是外部  
- 简写方式  
list-style:type image position;  

项目中最常用的写法list-style:none;**去掉列表标识**

## CSS3 CORE

### 复杂选择器

#### 兄弟选择器

兄弟元素：具有相同父元素的平级元素  
兄弟选择器，只能找弟弟，不能找哥哥  

- 相邻兄弟选择器  
获取紧紧挨在某元素后面的兄弟元素  
`选择器1+选择器2{}`
- 通用兄弟选择器  
获取某元素后，所有符合要求的兄弟元素  
`选择器1~选择器2{}`

#### 属性选择器  

id class style title name value width.......  
允许通过元素所附带的属性，及其值来匹配页面元素，很精准

- [attr] attr代表任意属性  
匹配页面中所有带attr这个属性的元素  
`[id]{}`     `[id][title]{}`
- elem[attr]  
匹配页面中所有带attr属性的elem元素  
`p[title]{}`   `p[id][title][class].....{}`  
- elem[attr=value]  
匹配页面中带attr属性，并且值为value的elem元素  
`div[title="woyouyeye"][class="c"]{}`  
- 模糊属性值匹配  
`[attr^=value]{}` 匹配attr的值以value开头的元素  
`[attr$=value]{}` 匹配attr的值以value结尾的元素  
`[attr*=value]{}` 匹配属性值中，有value的元素  
`[attr~=value]{}` 匹配属性值中，有value这个独立单词的元素  

#### 伪类选择器

:link :visited :hover :active :focus 已经学过的伪类  

- 目标伪类(锚点)  
让被激活的锚点，应用样式  
`选择器：target{}`
- 结构伪类  
  - `elem:first-child{}`  
 代表两个条件:  
匹配elem的父元素的第一个儿子（elem的大哥）  
这个大哥必须是elem元素  
  - `elem:last-child{}`  
匹配elem的父元素的最后一个儿子(elem的小弟)
这个最小的弟弟必须是elem元素
  - `elem:nth-child(n)`  
匹配elem的父元素的第n个儿子(n从1开始)
这个儿子也必须是elem元素

- 匹配空元素  
`:empty{}`  
空元素：没有文本，没有空格，没有其他子元素的元素
- `:only-child`  
匹配，当前元素是其父元素的唯一的子元素  
- 否定伪类  
`:not(selector)`  
/*除了第一个a标签，其它a的字体都变成黄色*/  
`a:not(:first-child){color:#ff0;}`  
/*除了第三个a标签，其它a的字体都变成蓝*/  
`a:not(:nth-child(3)){color:#f0f;}`  

#### 伪元素选择器

- 内容伪元素(**操作的不是标签，是标签中的内容**)
  - `::first-letter{ }` 或 `:first-letter{}`  
 匹配首字符的样式
  - `::first-line{ }` 或 `:first-line{}`  
 匹配首行的样式  
 **当首行和首字符冲突的时候，以首字符为准**
  - `::selection{}` **必须是两个 ::**  
 匹配选中部分的文字样式  
 **注意：只能改变字体颜色和背景颜色**
- 伪元素选择器，**内容生成**  
**使用css，添加httml元素，称之为伪元素内容生成**  
`:before` 或者 `::before`  
匹配到某个元素的内容区域的最前面，添加一个内容，  
content：添加的文本或者图片  
display：是设置这个添加的内容的显示规则  
`::after` 或者 `:after`  
匹配到某个元素的内容区域的最后面，添加一个内容  
注意：**content中，只能添加文本或者图片**  
可以理解为在内容区域中，最前或者最后面，添加了一个元素。  
这个元素的显示方式，由display来设定  

##### 伪元素内容添加，可以解决的问题

- 解决外边距溢出  

```css
 #parent::before{
  content:"";
  display:table;
 }
```

- 解决高度坍塌  
定位造成的高度坍塌此办法不能解决(可以通过设定高度解决)，  
因为定位没有`clear:both;`

```css
#d1:after{
      content:"";
      display:block;
      clear:both;
}
```

## 弹性布局（重点*******************************************）

>什么是弹性布局  
是一种布局方式  
主要解决某个元素中子元素的布局方式  
为布局提供很大灵活性  

### 弹性布局相关的概念和名词解释

![弹性布局.png](https://i.loli.net/2019/07/29/5d3ed279b245337708.png)

1. 容器  
要发生弹性布局的子元素，他们的父元素称之为容器  
容器要设置属性display:flex;  
2. 项目  
要发生弹性布局的子元素们，称之为项目  
就是设置了display:flex那个元素的，子元素们  
3. 主轴  
项目们在容器中排列的**方向**，就是主轴  
如果项目横向排列，x轴就是主轴  
如果项目纵向排列，y轴就是主轴  
项目们的排列顺序，靠主轴的起点和主轴的终点来定义  
4. 交叉轴  
与主轴垂直相交的一条轴，叫做交叉轴  
项目们在交叉轴上的对齐方式，是交叉轴的起点和终点  

### 弹性布局语法

display，写在父元素中  

- 取值：  

  - flex 将块级元素设置为容器  
  - **inline-flex 将行内元素设置为容器**  
- 特点：  
  - 弹性项目，默认x是主轴，主轴起点在左侧(块级元素横向排列的第二个解决方案)  
  - 项目的float/clear/text-align/vertical-align属性失效
  - 每个项目可以自由的设置尺寸  
- 容器的属性  
  - 主轴的方向:flex-direction:  
取值：  
    - row默认值，主轴是x轴，主轴起点是左端
    - row-reverse,主轴是x轴，主轴起点是右端
    - column 主轴是y轴，主轴起点是顶端
    - column-reverse 主轴是y轴，主轴起点是底部
  - 设置项目换行:flex-wrap:  
取值  
    - nowrap 默认值，容器空间不够，也不换行，项目自动缩小
    - wrap 空间不够就换行
    - wrap-reverse 换行并反转
  - 主轴方向，项目换行的缩写:flex-flow:  
取值  
    - direction wrap
  - 定义项目在主轴上的对齐方式:justify-content:  
取值  
    - flex-start 默认值，以主轴起点对齐
    - flex-end 以主轴终点对齐
    - center 在主轴上居中对齐
    - space-between 主轴两端对齐，两端无空白
    - space-around 每个间距大小相同
  - 项目在交叉轴上的对齐方式：align-items:  
取值  
    - flex-start 交叉轴起点对齐
    - flex-end 交叉轴终点对齐
    - center 交叉轴居中对齐
    - baseline 交叉轴基线对齐
    - stretch **前提，项目不写高**，占满交叉轴上所有的空间
- 项目的属性
  - order  
定义项目的排列顺序  
取值，无单位整数，值越小，越靠近主轴起点  
  - flex-grow  
定义项目的放大比例  
如果容器有足够大的剩余空间，项目将按比例方大  
取值：无单位的数字  
  **默认值0，不放大**  
  - flex-shrink  
定义项目缩小的比例，容器空间不够时，项目该如何缩小  
取值：无单位数字  
取值越大，缩小比例越大。  
**默认值:1**;**0:不缩;**  
  - align-self  
设置此项目在交叉轴上的对齐方式，不影响其它项目  
取值：  
    - flex-start
    - flex-end
    - center
    - baseline
    - stretch
    - auto 使用容器定义的align-items的值

## CSS hack

>由于不同的浏览器对css的解析认知不同，会导致同一份css在不同浏览器中生成页面效果不同  
面对这种情况，开发人员需要针对不同浏览器写不同的css  
这个行为，就叫做css hack  

```css
div{
  background:-webkit-linear-gradient(....);
  background:-o-linear-gradient(....);
  background:-ms-linear-gradient(....);
  background:-moz-linear-gradient(....);
}
```

tmooc有css hack相关拓展视频

## 转换（重点**************************）

>转换:改变元素在页面中的位置，大小，角度，以及形状

2D转换:只在x轴和y轴发生的转换效果  
3D转换:增加了z轴的转换效果。3D是模拟出来的  

### 转换的属性

#### transform

取值  

- none 默认值，无任何转换效果
- transform-function 转换函数  
       表示1个或者多个转换函数  
       如果是多个转换函数，每个函数之间用空格分开  
       transform:translate(400px) rotate(90deg);  
学习转换，就是学习转换函数  

#### 转换原点

transform-origin:  

取值：  

- 以px为单位的数字
- %
- 关键字 x(left/center/right)  y(top/center/bottom)  

取值个数：  

- 2个值，原点在x轴和y轴上的位置
- 3个值，原点在x轴，y轴和z轴上的位置  
**默认值 center center**

#### 2D转换

- 位移（改变元素的位置）  
`transform:translate(参数)`  
参数：  
  - translate(x) 等同于translateX(x)  
        指定元素在x轴上的位移距离  
         +  往右       - 往左  
  - translate(x,y)指定元素在x轴和y轴上的位移距离  
         x: +  往右       - 往左  
         y:+  往下        - 往上  
  - translateX(x)  
  - translateY(y)  
取值：  
    - px为单位的数字
    - %
- 缩放(改变元素的尺寸)  
`transform:scale(value)`  
取值  
  - 一个值  
    - value>=1  x轴和y轴都放大的倍数
    - 0<value<1 x轴和y轴都缩小
    - -1<value<0 x轴和y轴都缩小，并反转(以对应轴为旋转轴)180度
    - value<=-1 x轴和y轴放大，并反转180度
  - 两个值  
    scale(x，y) 分别设置x轴和y轴的放大比例
  - scaleX(x) 单独设置x轴
  - scaleY(y) 单独设置y轴
- 旋转(改变元素的角度)  
`transform:rotate(190deg)`  
取值：  
  - \+ 顺时针旋转  
  - \- 逆时针  
 先旋转45deg,再位移300px？VS先 位移300px，再旋转45deg？  
注意：旋转原点会影响效果  
     **旋转是连同坐标轴一起旋转的，会影响旋转之后的位移方向**  
- 倾斜  
  - skew(x) 等同于 skewX(x)  
  让元素向着x轴发生倾斜，实际上改变的是y轴的角度  
  x:+  逆时针倾斜  \-  顺时针倾斜  
![skew(x).png](https://i.loli.net/2019/07/30/5d3fa1c1a8f5a22360.png)
  - skewY(y)  
让元素向着y轴发生倾斜，实际上改变的是x轴的角度  
  y:+ x轴顺时针倾斜 \- x轴逆时针倾斜
![skew(y).png](https://i.loli.net/2019/07/30/5d3fa1bda435440882.png)

#### 3D转换---3d都是模拟

##### 透视距离 perspective

模拟人的眼睛到3D转换元素之间的距离，透视距离不同，看到的效果不同  
设置透视距离,perspective:距离，  
**此属性要加载到3d转换元素的父元素上**  

##### 3D旋转

属性：transform  
取值：  

- rotateX(xdeg)  
       以x轴为中心轴旋转，烤羊腿  老式爆米花机
- rotateY(ydeg)  
       以y轴为中心轴旋转，旋转门，旋转木马，钢管舞
- rotateZ(zdeg)  
       以z轴为中心轴旋转,风扇，风车，摩天轮
- rotate3D(x,y,z,ndeg)  
        **x,y,z取值0，代表这条轴不参与旋转**  
            **取值>0, 表示该轴参与旋转**  

## 过渡（重点*****************）

>过渡:
让css属性的值，在一段时间内平缓变化的效果

### 过渡语法

#### 指定过渡的属性

transition-property  
取值：  

- 直接写css的属性，多个属性值之间用空格分开  
- all  所有支持过渡的属性，都参与此次过渡效果  

哪些属性支持过渡:

- 颜色属性
- 大多数取值为具体的数字的属性
- 阴影
- 转换transform **所有的转换，默认有过渡，一定走过渡**
- visibility

#### 指定过渡时长

transition-duration  
指定用多长时间完成此次过渡操作  
取值 ：s/ms为单位的数字  

#### 过渡时间曲线函数

transition-timing-function:  
取值  

- ease  默认值，慢速开始，中间变快，慢速结束
- linear 匀速
- ease-in 慢慢开始，快速结束
- ease-out 快速开始，慢慢结束
- ease-in-out 慢速开始，慢速结束，中间先加速后减速

#### 过渡的延迟时间

transition-delay:  
让过渡效果，延迟多少时间执行  
取值:  s/ms为单位的数字

#### 过渡代码的编写位置

- 原始选择器中(起点位置)，过渡效果有去有回
- :hover中(终点位置)，过渡效果有去无回

#### 简写方式

transition：property duration timing-function delay;  
最简方式：transition:duration;  

## 动画

>元素从一种样式逐渐变为另一种样式  
其实就是多个过渡效果放到一起

### 使用关键帧来控制动画的每一个状态

关键帧  

- 动画执行的时间点
- 在这个时间点上的样式

### 使用动画

- 使用关键帧定义动画

```css
@keyframes 动画名称{
  /*关键帧*/
 0%{样式}
 ...
 50%{样式}
 ..
 100%{样式}
}
/* ex: */
@keyframes liangjump{
  0%{transform:translate(0px,0px);}
  20%{transform:translate(0px,200px);}
  40%{transform:translate(0px,0px);}
  60%{transform:translate(0px,150px);}
  80%{transform:translate(0px,0px);}
  100%{transform:translate(0px,110px);}
}
```

- 调用动画  
  - 调用动画名称  
animation-name:动画名称
  - 设置动画执行时间  
animation-duration: s/ms
  - 设置动画的时间曲线函数  
animation-timing-function
  - 设置动画延迟播放  
animation-delay:2s;

- 动画的其它属性  
  - 设置动画的播放次数  
animation-iteration-count:  
取值  
    - 具体次数，无单位数字
    - infinite 无限
  - 设置动画的播放顺序  
animation-direction:  
取值：  
    - normal 默认 0%~100%
    - reverse 100%~0%
    - alternate 轮流播放，第一遍正向，第二遍逆向，...

- 动画的简写方式  
animation：name duration timing-function delay count direction  
最简方式 animation:name duration;

- 设置动画，播放前后的状态  
animation-fill-mode  
取值：  
  - backwards，动画播放之前的延迟时间内，显示第一帧
  - forwards，动画播放完成，保存在最后一帧
  - both,同时使用backwards和forwards
  - none 默认值，不填充

- 设置动画的播放状态  
animation-play-state  
取值：  
  - paused 暂停
  - running 播放

```html
<style>
   #d1{
   width:100px;height:100px;
   background-image:url(chengliang.jpg);
   background-size:100%;
   border-radius:50%;
  }
   /*使用关键帧定义动画*/
   @keyframes liangjump{
         0%{transform:translate(0px,0px);}
         20%{transform:translate(0px,200px);}
         40%{transform:translate(0px,0px);}
         60%{transform:translate(0px,150px);}
         80%{transform:translate(0px,0px);}
         100%{transform:translate(0px,110px);}
   }
   #d1:hover{
         /*调用动画*/
         animation-name:liangjump;
         animation-duration:2s;
   }
</style>
<body>
    <div id="d1"></div>
</body>
```

### 动画的兼容性

如果要兼容低版本浏览器，需要在动画声明的时候加前缀

```css
@keyframes 动画名称{}
@-webkit-keyframes 动画名称{}
@-o-keyframes 动画名称{}
@-moz-keyframes 动画名称{}
@-ms-keyframes 动画名称{}
```

## CSS优化

- CSS优化的目的  
  - 减少服务器压力
  - 提升用户体验
- CSS优化原则
  - 尽量减少http的请求个数  .css .js .jpg
  - 在页面顶部，引入css文件
  - 将css和js文件放到外部独立的文件中
- CSS代码优化
  - 合并样式（能简写，就不分开写.能写群组，就不单写）
  - 缩小样式文件的大小（能重用的样式，尽量重用）
  - 减少样式重写
  - 避免出现空的href和空的src  
  - 选择更优的样式属性
  - 代码压缩

## 响应式布局(css3)

>响应式网页  
Responsive web page 响应式/自适应网页  
可以根据浏览网页的设备不同(pc,pad,phone)  
而自动改变布局，文字，图片效果。  
不会影响用户体验  

### 响应式网页必须保证几件事情

- 布局，不能固定元素宽度.必须是流式布局(默认文档流+浮动)
- 文字和图片大小随着容器的大小而改变
- 媒体查询技术(css3的技术)

### 如何测试响应式网页

- 使用真实设备测试  
  好处：真是可靠  
  缺点：成本高，测试任务巨大  
- 使用第三方测试软件  
  好处：不需要太多真实设备，测试方便  
  坏处：测试效果有限，有待进一步验证  
- 使用chrome等浏览器自带的模拟软件  
  好处：简单方便  
  坏处：测试效果十分有限，需要进一步验证  

### 编写响应式布局(重点**************************)

- 手机适配,设置视口
只有移动端设备，需要设置视口  
`<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">`  
viewport 视口  
width=device-width  视口宽度等于设备宽度  
initial-scale=1.0 设置视口宽度能否缩放  1.0不能缩放  
maximum-scale=1.0 允许视口缩放的最大倍率  1.0不缩放  
user-scalable=0 是否允许用户手动缩放  0不能  
最简洁的写法  
`<meta name="viewport" content="width=device-width, initial-scale=1">`  
- 所有内容/文字/图片都尽量使用相对尺寸，不要使用绝对数字
- 流式布局+弹性布局+媒体查询，组成响应式布局
- 媒体查询: CSS3 Media Query  
媒体查询是写响应式必须具备的技术  
Media：媒体，不同的用于浏览网页的设备  
    设备：  
  - screen（pc/pad/phone）  
    - \>=1200px --> xl
    - 1200~992px --> l
    - 992~768px --> m
    - 576~768px --> s
    - 576px --> xs
  - TV  
  - print  

>Media Query:可以自动的根据当前浏览设备不同(尺寸，方向，解析度。。。)，有选择性的，执行一部分代码，忽略其他代码

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <style>
      body {
        font: 16px chiller;
        padding: 0;
        margin: 0;
      }
      /*pc>=992     大屏，字体红色，背景黑色*/
      @media screen and (min-width: 992px) {
        #content {
          color: #f00;
          background: #000;
        }
      }
      /*768<=pad<992中屏，字体黄色，背景红色*/
      @media screen and (min-width: 768px) and (max-width: 991px) {
        #content {
          color: #ff0;
          background: #f00;
        }
      }
      /*phone<768   小屏，字体黑色，背景蓝色*/
      @media screen and (max-width: 767px) {
        #content {
          color: #000;
          background: #0ff;
        }
      } /* 11:16~~11:31休息 */
    </style>
  </head>
  <body>
    <div id="content">
      <h1>媒体查询，根据浏览设备不同(尺寸,方向)，加载不同的css代码</h1>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Minus ipsa
        nulla saepe vitae nam debitis quisquam dolores odit nobis repudiandae
        eaque provident possimus tempore et alias aliquam assumenda laboriosam.
        Asperiores esse iure officia enim saepe autem laborum incidunt maiores
        dolor porro. Ipsum accusantium repudiandae assumenda et id temporibus
        voluptas quasi minima in inventore debitis facilis. Temporibus hic ullam
        fugiat aperiam pariatur at quisquam error ut necessitatibus nulla itaque
        explicabo repellat ipsa molestiae consequuntur! Minus adipisci provident
        deleniti sint fuga ipsa recusandae. Quo libero impedit et nam incidunt
        laborum voluptatem placeat autem debitis perspiciatis molestias
        consequuntur assumenda cumque in alias maiores esse enim dignissimos
        officiis iusto eaque neque molestiae magnam atque consectetur dolorem
        rem sed. Repellat voluptates repudiandae natus dicta tenetur suscipit
        temporibus obcaecati blanditiis nostrum modi quaerat perspiciatis
        molestias id. Ullam iste enim odio necessitatibus optio a quod
        repellendus itaque quidem quam! Fuga harum aperiam sed soluta aut
        corrupti libero officiis consectetur tenetur incidunt animi eos
        laudantium quo earum quos nulla labore omnis repudiandae obcaecati
        eaque. Inventore fugiat dignissimos nobis qui natus ratione accusantium
        ex architecto neque facilis quod deleniti voluptates. Exercitationem
        consequatur ullam totam ipsum fugit quam laboriosam eligendi dolores
        similique corporis praesentium id rerum dolorum qui nesciunt beatae nemo
        neque reiciendis. Recusandae exercitationem nulla reiciendis dicta iste
        natus accusantium delectus sed provident a. A nobis hic aliquid sequi
        veniam maiores perferendis accusamus quam ex quasi pariatur facere
        dolore consequuntur ipsa laboriosam illum maxime! Porro accusamus
        aliquam explicabo sapiente exercitationem earum inventore saepe
        dignissimos iusto autem rem ex. Optio perferendis molestias consequuntur
      </p>
    </div>
  </body>
</html>
```

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <style>
      div {
        border: 2px solid #f00;
        /*媒体查询布局，经常要定义border-box*/
        box-sizing: border-box;
      }
      #d1,
      #d2,
      #d3 {
        float: left;
        color: #f00;
        font: 36px chiller;
      }
      #content:after {
        content: "";
        display: block;
        clear: both;
      }
      /*pc>=992px 横向显示3个 1:2:1*/
      @media screen and (min-width: 992px) {
        #d1 {
          width: 25%;
          height: 400px;
        }
        #d2 {
          width: 50%;
          height: 400px;
        }
        #d3 {
          width: 25%;
          height: 400px;
        }
      }
      /*768<=pad<992px  1.50% 2.50%  3.none*/
      @media screen and (min-width: 768px) and (max-width: 991px) {
        #d1 {
          width: 50%;
          height: 400px;
        }
        #d2 {
          width: 50%;
          height: 400px;
        }
        #d3 {
          display: none;
        }
      }
      /*phone<767px 3个div竖着显示*/
      @media screen and (max-width: 767px) {
        #d1 {
          width: 100%;
          height: 200px;
        }
        #d2 {
          width: 100%;
          height: 200px;
        }
        #d3 {
          width: 100%;
          height: 200px;
        }
      }
    </style>
  </head>
  <body>
    <div id="content">
      <div id="d1">
        1~Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptate
        repudiandae.
      </div>
      <div id="d2">
        2~Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptate
        repudiandae.
      </div>
      <div id="d3">
        3~Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptate
        repudiandae.
      </div>
    </div>
  </body>
</html>

```
