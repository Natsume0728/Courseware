# QUESTION

- margin 属性  
块级元素的垂直相邻外边距会合并，而行内元素实际上不占上下外边距。  
行内元素的的左右外边距不会合并。同样地，浮动元素的外边距也不会合并。
  - margin:10px 5px 15px 20px; 上 右 下 左；
  - margin:10px 5px 15px; 上 (右 左) 下 ；
  - margin:10px 5px; ( 上 下) ( 左 右)；
  - margin:10px;

- CSS选择器
  - div>p：选择父元素为 \<div> 元素的所有 \<p> 元素。
  - div+p: 选择紧接在 \<div> 元素之后的所有 \<p> 元素。
  - div p: 选择 \<div> 元素内部的所有 \<p> 元素。
  - iv,p: 选择所有 \<div> 元素和所有 \<p> 元素。

- css a标签占满父级元素
width: 100%;
height: 100%;
display: block;

- 使用伪元素清除浮动解决高度塌陷  

```scss
.father:after {
  content: ""; //为伪元素添加空的内容
  display: block; //将伪元素转化为块级元素
  clear: both; //清除两侧的浮动
}
```
