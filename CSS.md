# CSS

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
   1. 样式代码可以高度重用，html属性不能重用
   1. 方便后期维护，提高可维护性。

## css的语法规范

1. 使用css样式的方式
   - 行内样式(内联样式)  
在html标签的style属性中，编写样式  
语法：<any style="样式声明"></any>  any:任意标签  
样式声明：样式属性 : 值  
有多个样式声明：样式属性1：值1 ；样式属性2：值2  
ex:  
\<div style="color:red;background-color:yellow">  
内联样式在项目中，很少使用,学习和测试的时候用。  
原因：  
     1. **内联样式不能重用**  
     1. **内联样式优先级最高**  
目前常用的样式：  
color:orange; 字体颜色  
background-color:yellow; 背景颜色  
font-size:36px； 字号大小  
   - 内部样式  
在网页头部中，添加一对\<style>\</style>标签  
在style标签中定义此网页所有的样式  
\<style>  
   选择器{样式属性：值；样式属性：值；........}  
\</style>  
选择器：就是一个条件，符合这个条件元素，可以应用这个样式  
项目中使用内部样式较少，学习和测试使用较多。  
内部样式的重用不能在其他html页面中生效  
   - 外部样式  
单独创建一个css文件，编写样式  
在html页面的head中使用link，引入这个外部样式  
\<link rel="stylesheet" href="css文件的url">  
注意：rel="stylesheet"必须写，不然无效;  
此种方式，是开发中使用最多方式。  
  练习  
01_ex.html  
h1 内容随意，内联，背景为粉色pink，字体为yellow  
h2 内容随意，内部，背景为粉色yellow，字体为red  
h3 内容随意，外部，背景为粉色red，字体为blue  
1. CSS的特性
   1. 继承性  
**大部分的css效果，是可以被子元素继承的;**  
**必须是父子结构，子继承父;**  
   1. 层叠性  
**可以为一个元素定义多个样式规则;**  
**多个规则中样式属性不冲突时**，可以同时应用到当前元素上;  
   1. 优先级  
如果对一个元素的多个样式声明，发生冲突时，按照样式规则的优先级去应用;  
默认优先级：由高到低  
       1. 内联样式(行内样式)  
       2. 内部样式和外部样式，就近原则
       3. 浏览器默认样式
   1. 调整优先级  
!important规则  
放在属性值后面，与值之间有一个空格;  
作用，调整样式显示的优先级;  
内联样式不可以写!important ;  
!important优先级，比内联样式高;  

 练习  
02_ex.html中  
一个p标签，内容假文lorem  
用内部样式设置文本颜色为蓝色，字号24px  
用外部样式设置文本颜色为 红色，字号40px  
让外部样式引入，F12查看页面效果  
然后对调内部样式和link的位置，F12观察结果  
尝试使用!important调整样式优先级  

## 基础选择器(重点！！！！！！)

>选择器的作用:  
规范了页面中哪些元素能够使用定义好的样式,  
选择器就是为了匹配元素用,  
(选择器是一个条件，符合这个条件的元素就可以使用这个样式)  

### 选择器详解

01. **通用选择器**  
*{样式声明}  
由于*的效率低下，项目中很少使用通用选择器;  
唯一使用的场合*{margin:0;padding:0}所有元素内外边距清零；  
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
  练习:  
03_ex.html h2标签，内容随意(假文)，这个h2标签id为text1  
使用id选择器设置文本为purple，背景yellow，  
字体为斜体font-style:italic；查看页面观察效果  
再使用元素选择器，设置文本为红色，背景pink。  
这里有坑，会对就近原则产生怀疑，选择器权值问题  
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
\<div class="text-danger bg-warning font-24">d\</div>  
     1. 分类选择器  
        - 元素选择器+类选择器{}  
div.text-danger{ }  
div元素有text-danger类,才能应用这个样式  
        - 类选择器+类选择器{}  
.font-24.text-danger{ }  
元素，必须有font-24类和text-danger，才能应用此样式  
作用：  
1.更精确的确定使用样式的元素  
      2.增加选择器的权值  
 练习  
04_ex.html 页面中有div和p元素，内容假文随意  
用类选择器设置字体颜色为红色，注意类名的命名规范  
用分类选择器为p元素设置背景色为green  

05. **群组选择器**  
将多个选择器放在一起定义公共的样式  
语法：选择器1,选择器2,......{公共样式声明}  
ex:  
\#content,div,.mycolor,p.text{color:red}  
相当于  
\#content{color:red}  
div {color:red}  
p.text {color:red}  
.mycolor {color:red}  
06. **后代选择器**  
通过元素的后代关系匹配元素  
后代：一级嵌套或者多级嵌套  
语法：选择器1  选择器2  选择器3........{}  
\#content p span{color:red;}  
id为content的元素，内部不管隔着多少代，有一个p元素  
p元素内部，不管隔着多少代，有一个span，这个span就符合要求  
7. **子代选择器**  
通过元素的子代关系匹配元素  
子代：一级嵌套，直接的儿子  
选择器1>选择器2>....{}  
子代选择器和后代选择器可以混写  
\#content p>span{background-color:yellow;}  
 练习  
05_ex.html  
ul#content>li*4>span>a  
a标签字体36px，字体颜色red，背景颜色yellow  
使用后代或者子代选择器，至少3种选择器写法  
8. **伪类选择器**  
匹配同一个元素，不同的状态下的样式  
所有的伪类选择器都是这样开头的: **选择器：**  
   1. 链接伪类  
      - a标签，没有访问的状态===> a:link{color:red;}  
      - a标签，被访问过之后的状态===> a:visited{color:black;}  
   1. 动态伪类  
      - :hover 鼠标悬停在元素上时，元素的样式
      - :active 匹配元素被激活时的状态
      - :focus 匹配元素获取焦点时的状态  

 练习  
1.06_ex.html  
一个a标签，内容随意，href随意-------------坑  
    1.访问后，文本颜色orange  
    2.被激活时，文本颜色绿色  
    3.鼠标悬停时，文本颜色红色  
    4.未被访问时，文本pink  
2.页面在红添加一个input--text  
  默认字体为gray，font-style:italic；  
  1.被激活时，字体不斜：font-style:normal;  
  2.获取焦点时：文本为红色  

**选择器的权值**  
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
3. 群组选择器的权值，单独各算各的，不能相加;  
4. 样式后面追加!important直接获取最高优先级;  
  内联样式不能加!important  
5. 选择器的权值计算，结果不会超过自己的最大数量级;  
(1000个1相加，也不会大于10)

作业1：  
css使用方法3个  
        css特性3个  
        选择器8个  
        权值  
        上述知识点的demo重做一遍  
作业2：  
重新完成学子注册模块  

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
**但是，自带宽高属性的行内元素，可以设置尺寸**  
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
width:边框的宽度，取值以px为单位的数字  

style:边框的样式 取值：  

- solid实线  
- dotted 点点虚线  
- dashed 线状虚线  
- double 双实线  

color：边框的颜色  
取值 合法的颜色值/transparent(透明)  
最简方式 border:style;  
取消边框 border:0;  或者 border:none;  

  练习
03_ex.html  
3个div,给每个div设置边框，每个div  10px*10px  
第一个 1px 实线 红色  
第二个 5px 点虚线 蓝色  
第三个 10px 线虚线 黄色  

#### 单边定义边框

只设置某一条边的3个属性  
border-top：width style color;  
border-right  
border-bottom  
border-left  

 练习  
03_ex中，div#d4 200px*200px  
上边框，3px实线 红色  
右边框  5px 点 蓝色  
下边框  10px 线虚线 黄色  
左边框  15px  双实线 #f0f  

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

 练习  
画柠檬/芒果  

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
练习
圆形发光体 太阳，吸顶灯，日食，月食

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

练习
05_ex  
两个div，尺寸300px*300px  
背景色随意。  
设置两个div之间的间距是50px，  
两个div都水平居中  

#### 外边距的特殊效果  

- **外边距合并**

两个垂直外边距相遇时，他们将合并成一个，值以大的为准,  
只能在布局设计的时候，尽量避免发生  

作业  
1：坑  
页面中两个div，宽高200px,分别设置背景颜色  
为两个div设置4个方向外边距，观察效果  
与div平级，添加两个span，内容随意，分别设置背景颜色  
为两个span添加4个方向外边距，观察效果  
与div平级，添加两个input-text，  
为两个input添加4个方向外边距，观察效果  
2.坑  
div#d1>div#d2  
\#d1宽高300px  
\#d2宽高100px  
分别设置背景颜色  
给#d2设置上外边距，观察效果  
3.今天所有知识点的demo  
4.ajax 登录模块/注册模块/查询用户列表/删除/  

 练习
01_ex  
1.两个div 200px*200px 背景颜色不同  
  为两个div单独设置4个方向外边距  margin-方向  
2.两个span，内容随意，背景颜色不同  
  为两个span单独设置4个方向外边距  
3.两个文本框，  
 为两个input单独设置4个方向外边距  

- **关于块级元素，行内元素，行内块的外边距总结**  
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
- **自带外边距的元素**  
body h1~h6 p ol ul dl pre  
由于不同浏览器对默认的外边距解析可能有差别  
所以一般情况下，开发之前，需要把内外边距清空  
\*{margin:0;padding:0}  
或者通过群组选择器来写  
blockquote,body,button,dd,dl,dt,fieldset,form,
h1,h2,h3,h4,h5,h6,hr,input,legend,li,ol,
p,pre,td,textarea,th,ul{margin:0;padding:0}  

 练习  
01_ex  
div#d3 尺寸300px*300px  
\#d3中有div#d4 100px*100px  
两个div不同背景颜色。  
给#d4设置上外边距，在f12中改变上外边距的数值  
观察效果  

- **外边距溢出**  
在特殊情况下，为子元素设置外边距，会作用到父元素上  
特殊情况：  
1.父元素没有上边框  
2.子元素内容区域上边与父元素内容区域上边重合的时候  
(为父元素中第一个子元素设置上外边距时，这种说法不严谨)  
解决方案：  
1.给父元素添加上边框，弊端，影响父元素实际占地高度  
2.给父元素添加上内边距，弊端，影响父元素实际占地高度  
3.给父元素的一个子元素的位置添加空table元素  

### 内边距

内边距的改变效果，感觉是改变了元素的大小  
不会影响其它元素，但是真正改变的是本元素的占地尺寸  
内边距颜色和元素背景相同  

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
            2. px为单位的数字，半径失效
    - 重复渐变  
重复的线性渐变  
background-image:  
repeating-linear-gradient(to left,#000 0px,#ff0 25px,#000 50px);
重复的径向渐变
background-image:
repeating-radial-gradient(50px at center center,
\#000 0%,#0ff 25%,#000 50%);  
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

 练习  
01_ex  
定义div，内容随意，假文，有中文  
1.设置字体系列  
2.设置字号 大小  
3.加粗并斜体  
4.所有小写字母转为小型大写字母  
5.两端对齐  
6.文本有下划线  
7.首行缩进30px  
8.文本垂直居中  

## 表格的样式

1. 表格的常用样式属性table>tr>td  
    - table:之前学习过的样式，基本都可以使用  
尺寸，边框，背景，字体，文本，内外边距  
给table设置border,只设置最外面的大边框  
    - td/th的样式  
尺寸，边框，背景，字体，文本，内边距  
外边距无效  
vertical-align指定单元格数据的垂直对齐方式  
取值：  
top/middle/bottom  

练习  
02_ex  
创建4*4表格，宽高400px。内容随意  
1.设置每个单元格的尺寸为100px*100px  
2.设置每个单元格边框1px solid #000  
3.尝试给每个单元格设置上外边距20px.上内边距20px；  
>表格是一种特殊的表现方式  
表格实际尺寸是根据内容数据的多少而决定的
单元格小，内容多，自动撑开
内容少，单元格就按照设置的尺寸来展示

2. 表格特有的样式属性  
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
    - 设置表格的显示规则  
用来确定如何布局一张表格  
table-layout  
取值  
        - auto 默认值  
        自动布局表格  
            列的尺寸实际使用内容决定的，内容比尺寸大，按照
            内容大小显示。  
            内容比尺寸小，按照尺寸显示
        - fixed  
        固定表格布局，列的尺寸以设置的为准

### 自动布局与固定布局

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

#### 普通流定位

又称为默认文档流定位  

1. 每个元素在页面上都有自己的空间
2. 每个元素都是从父元素的左上角开始渲染（显示）
3. 块级元素按照从上到下逐个排列，每个元素单独成行
4. 行内元素是多个元素在一行中显示，从左往右顺序排列，显示不下换行

#### 浮动定位

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
2. 浮动元素会在当前行，停靠在父元素的左/右边，或者停靠在其他已浮动元素的边缘
3. 当父元素横向显示不下所有浮动元素时，最后显示不下的，会自动换行
4. 浮动用于解决，多个块级元素在同一行显示的问题

#### 浮动定位引发的特殊情况

1. 浮动元素占位的问题  
 当元素显示不下所有浮动元素时，最后显示不下的元素会换行  
 但是，已浮动元素会根据自己的浮动方向占据位置，  
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

一个页面中，编写css的思路
从上往下，从左往右，从外往里
1.尺寸，大体位置
2.边框，背景相关
3.文本相关
4.微调