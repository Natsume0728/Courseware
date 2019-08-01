# SASS

>CSS有很多缺点  
语法不够强大，没有变量，没有合理的样式复用机制  
导致难以维护  
>>使用动态样式语言，赋予css新的特性
提高样式语言的可维护性

常用的动态样式语言  

- SCSS/SASS （scss兼容sass,scss更接近css语法）
- stylus
- less

>scss是一款强化css的辅助工具,它和css语法很像。  
它在css的语法基础上，添加了变量，嵌套，混合，导入，函数等高级功能。  
这些拓展命令让scss更加强大和优雅  
>>浏览器不能直接解析scss文件，需要在想项目中把scss转义成css文件，让浏览器解析
scss可以让css开发更高效

## scss的安装使用

>scss在服务器端使用
nodejs v8.11以上，才可以使用scss

- 在线安装scss  
在cmd中，输入命令npm install -g node-sass
- 无网络安装  
  找到sass的4个文件，  
  找到nodejs的安装路径,把sass4个文件放入node文件夹  
  在cmd中使用`node-sass -v` 验证版本  

### SCSS文件转换成css文件

- 单文件的转换
  1. 创建scss/01.scss文件
  2. 在项目路径下，打开黑窗口
  3. 输入下面命令 `node-sass scss文件路径 css文件路径`
![sass_01.png](https://i.loli.net/2019/07/30/5d3fdfb8ec83790298.png)
- 多文件转换  
文件夹--->文件夹  
`node-sass scss文件夹 -o css文件夹`
![sass_02.png](https://i.loli.net/2019/07/30/5d3fe0aa4055930991.png)
- 单文件监听转换  
`node-sass -w scss/01.scss css/01.css`
![sass_03.png](https://i.loli.net/2019/07/30/5d3fe1a10c07d79114.png)
- 多文件监听，监听一个文件夹中所有文件  
`node-sass -w scss文件夹 -o css文件夹`
![sass_04.png](https://i.loli.net/2019/07/30/5d3fe244d84c535383.png)

### SCSS基本语法

#### 变量

- 使用$声明变量，变量名可以包含"-","_";  
- 命名规则基本与css选择器相同，尽量做到见名知意;  
- 变量声明在{}外，整个scss文件都可以使用。  
- 变量声明在{}内，只有当前{}内可以使用。  
- ! default规则，如果此变量在之前已经声明赋值了，那么使用之前的值。  
如果之前没有声明赋值，使用现在值

#### 嵌套

- 选择器的嵌套  

```scss
#content{
  width:$my_width;
  div.top{
    margin:$my_width;
    h1{font-size:46px;}
    p{padding:12px;}
  }
  div.bottom{
    border: $my_border;}
}
```

自动转换成css的后代选择器

```css
#content {  width: 521px; }
#content div.top { margin: 521px; }
#content div.top h1 {font-size: 46px; }
#content div.top p {padding: 12px; }
#content div.bottom { border: 1px solid #00f; }
```

- 伪类的嵌套  
需要在伪类选择器之前添加&，如果不添加，会生成一个空格导致伪类失效  

```scss
a{width:21px;
  &:hover{width:20px}
}
```

- 属性的嵌套  

```scss
div{
  border:{style:solid;width:1px;color:#fff;};
}
```

- 群组选择器的嵌套

```scss
nav,div,header,footer{
   a{width:100px;}
}
```

#### 导入

>在scss的语法中，如果一个scss文件以下划线开头，  
那么这个scss文件就是一个**局部scss文件**  
scss文件转换成css文件的时候，不会把局部scss文件进行转换  
只转换，不以下划线开头的scss文件(全局scss文件)  

导入的语法 `@import "name"`;  
真正导入的文件名称  "\_name.scss" 掐头去尾  
导入时，不写"_",不写".scss"后缀  
局部文件被导入后，局部文件中的样式，会在全局文件转换的css中生成。  
同时，局部文件中声明的变量，可以在全局文件中使用  

#### 混合器

>把多个选择器都会使用的样式，封装进一个混合器
需要使用的这些样式选择器，可以调用这个混合器
实现代码的重用。

关键字  

- 声明混合器  @mixin 混合器名称(形参1，形参2){样式}
- 调用混合器  @include 混合器名称(实参1，实参2)

混合器使用场合---css hack

#### 继承

>一个选择器，可以使用另外一个选择器的所有样式

```scss
.my1{
  width:100px;height:100px;
}
.my2{
  background:#f00;
  @extend .my1;
}
```

转换之后，继承的表现方式，是群组选择器  

```css
.my1, .my2 {
  width: 100px;
  height: 100px; }
.my2 {
  background: #f00; }
```

#### 运算

>加减乘除余
如果必要，会在不同单位间转换(前提是scss能转)

- 加法  
\+ 除了做加法，还做字符串拼接  
字符串拼接的时候  
  - 如果用有引号的字符串拼接无引号的，结果带引号的
  - 如果用无引号的字符串拼接有引号的，结果不带引号
- 减法  
由于变量声明的时候可以使用-  
系统分不清楚 - 是不是属于变量名称  
所以写减法的时候，要在 - 前后添加空格  
`width:$my-w - $my-h;`
- 除法  
在scss中， / 的作用是分隔符  
只有下面几种情况，我们判定为除法  
  - 运算式的两边，有变量，或者函数返回值的时候，是除法  
  `width: $w/2;`
  - 运算式被( )包裹的时候，是除法  
  `height:(500px/2);`
  - 运算式是其他算术运算式的一部分的时候，是除法  
 `margin-left:5px+8px/2px;`

#### 字符串的插值操作  

使用`#{ }`在字符串中做插值  
`content: "liangliang ate #{50+32} baozis";`

#### 颜色的运算

`#112233+#445566=#557799`  
\#rrggb rgb(r,g,b) 都是分段计算，红+红 绿+绿 蓝+蓝  
**rgba的元素，需要透明度相同，才允许计算**
`background:rgba(11,22,33,0.6)+rgba(22,33,44,0.6);`

### 函数

- scss预定义很多函数，有些函数直接可以在css中使用  
rgba(r,g,b,alpha)  
hsl(h,s,l)  
hue:色调 取值0~360  3个色段 0~120 120~240 240~360  
saturation：饱和度 0.0%~100%  
lightness:亮度  0.0%~100%  
- 数学函数  
  - round(\$v) 四舍五入
  - ceil(\$v) 向上取整
  - floor($v) 向下取整
  - min(\$v1,\$v2....)
  - max(\$v1,\$v2....)
  - random 随机数
- 字符串  
  - unquote(\$v) 去掉双引号
  - quote(\$v)  加双引号
  - to_upper_case(\$str) 把\$str转成大写
  - to_lower_case(\$str) 把\$str转成小写
- 自定义函数  

```scss
@function get_msg($a,$b){
   @return  $a*$b+($a/$b);
}
div{
  width:get_msg(3,2)+px;
}
```

### 指令

```scss
@if(){}
@else if(){}
@else{}
```

![sass_05.png](https://i.loli.net/2019/07/30/5d3ff44d525ef36015.png)

**bool的小括号可以去掉**  
![sass_06.png](https://i.loli.net/2019/07/30/5d3ff44bcc88751606.png)