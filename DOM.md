# DOM

## 查找元素(4种方法)

### 1. 不需要查找就可以直接获得的元素

- document:    根节点对象
- \<html>根元素:    document.documentElement
- \<head>元素:    document.head
- \<body>元素:    document.body

### 2. 按节点间关系查找  

何时：如果已经获得一个节点对象，找周围附近的节点对象时  
节点树：包含 __所有网页内容__ 的完整树结构  
包括：2大类关系

1. 父子关系：4个属性
   - 节点.parentNode
   - 节点.childNodes  
返回多个直接子节点组成的 __类数组对象__ 可用下标访问指定位置的子节点  
   - 节点.firstChild
   - 节点.lastChild
1. 兄弟关系：2个属性
   - 元素.previousElementSibling
   - 元素.nextElementSibling  
__元素树的优点__：不包含看不见的空字符，不会受到空字符的干扰。  
__鄙视题__：遍历一个指定元素下的所有后代元素，找到符合条件的元素。

### 3. 按HTML特征查找

按节点间关系查找的缺点：必须先有一个节点，才能找周围的关系。  
解决办法：在还未获得元素的情况下，执行首次查找，用按HTML特征查找。  

1. 按id查找一个元素
var elem = document.getElementById('id值')  
__强调:__  
   1. 必须用document调用。
   2. 只能找到一个符合条件的元素，如果有两个id相同，只能找到第一个。
1. 按标签名查找多个元素
var elem = 任意父元素.getElementsByTagName('标签名')  
__强调:__
   1. 可以用任意父元素调用，用哪个父元素调用，就只在哪个父元素下查找
   2. 返回对个元素组成的类数组对象
   3. 不仅查找直接子元素，且查找所有后代
1. 按class名查找多个元素  
var elem = 任意父元素.getElementByClassName('class名')  
__强调:__
   1. 用任意父元素调用
   2. 返回多个元素组成的类数组对象
   3. 不仅查找直接子元素，且查找所有后代
   4. 仅靠其中一个class，就可以找到元素
1. 按name属性值查找多个元素
var elem = document.getElementByName('name值')  
专门用于查找表单中有name属性的表单元素  
__强调:__
   1. 只能用document调用
   2. 返回多个元素组成的类数组对象

### 4. 按任意选择器查找元素

1. 仅查找一个符合条件的元素:  
var elem=任意父元素.querySelector("选择器")  
__强调:__
   1. 用任意父元素调用  
如果采用指定父元素，调用函数时必须是相对于父元素内的相对选择器  
比如:  
`document.querySelector("table>tbody td:last-child ")`  
`table.querySelector("tbody td:last-child")`  
~~`table.querySelector("table>tbody td:last-child ")`~~  
   2. 只能返回1个元素
   3. 不仅查找直接子元素，且在所有后代中查找
2. 查找所有符合条件的元素:  
var elems=任意父元素.querySelectorAll("任意选择器")  
__强调:__
   1. 用任意父元素调用，缩小范围
   2. 可返回所有符合条件的元素的类数组对象
   3. 不仅查找直接子元素，且在所有后代中查找  
缺点: 用选择器查找，效率不如用HTML特征查找高  

__总结:__  

1. 如果只要一个条件，就能找到想要的元素时，首选按HTML特征查找
2. 如果查找条件复杂时，需要多个条件才能找到想要的元素时，就首选按选择器查找——简单！

----------------------------------------------------

## 修改(3种方法)

### 1. 内容

1. 获取或设置元素开始标签到结束标签之间的原始HTML代码片段: 元素.innerHTML  
1. 获取或设置元素开始标签到结束标签之间的纯文本内容: 元素.textContent  
   和innerHTML比较:
   1. 去掉了内嵌的标签
   2. 转义符号翻译为正文
1. 获取或设置表单元素的值:表单元素.value

### 2. 属性(3大类)

1. HTML标准属性: HTML标准中规定的属性
     比如: title, class, href, src, target, id  
2种:  
   1. 用最初的核心DOM函数(4个):  
var 属性值=元素.getAttribute("属性名");  
元素.setAttribute("属性名","属性值");  
var bool=元素.hasAttribute("属性名")  
元素.removeAttribute("属性名")  
   1. HTML DOM——核心DOM函数的简化版  
将所有的HTML标准属性都提前定义在了元素对象上，属性值暂时都是""。  
元素.属性  
比如:  
      - 获得属性值: 元素.属性  
      - 修改属性值: 元素.属性=值  
      - 判断是否包含属性: 元素.属性!==""  
      - 移除属性: 元素.属性=""  
__总结:__  
今后只要是HTML标准属性，都可用.访问  
__特例:__ class属性，虽然是标准属性，但不能直接用.访问  
         class是js的关键词。  
__解决办法:__ 今后，凡是使用class属性，一律更名为className,使用className等于使用class。  

1. 状态属性: disabled &nbsp; checked  &nbsp; selected  
特殊: 他们的值都是bool类型  
而核心DOM的4个函数只能操作字符串类型的标准属性  
所以，__状态属性只能用.访问！__
1. 自定义扩展属性:HTML标准中没有规定的，程序员自发添加的属性  
2个典型使用场景:
   1. 在客户端临时缓存数据，减少向服务器端发送请求的次数
   2. 代替其它选择器，用于选择触发事件的元素，绑定事件处理函数
如何使用自定义扩展属性:  
      1. 添加自定义扩展属性:  
         - 在html页面中写死: <ANY data-自定义属性名="值"  
比如:\<img src="1.png" data-m="m.png" data-l="l.png">  
         - 用程序动态设置: 只能用setAttribute，不能用.  
比如: img.setAttribute("data-m","m.png")  
结果:\<img data-m="m.png">
      2. 修改自定义扩展属性: 也只能用setAttribute()  
      3. 读取自定义扩展属性的值: 只能用getAttibute()  
         - 比如: var m=img.getAttribute("data-m") &nbsp;m="m.png"
__强调:__ 因为自定义扩展属性，只出现在页面中，不在内存中，所以，只能用getAttribute()&nbsp; setAttribute()...来访问，不能用.访问。

### 3. 样式

修改内联样式: 元素.style.css属性="值"  

- 比如: div.style.display="block">  
效果: \<div style="display:block">  
__强调:__

1. css属性名如果带-，要去横线变驼峰  
比如:  
   - z-index  ->  zIndex  
   - background-position -> backgroundPosition
1. 如果css属性值带单位，则必须加单位！  
问题: 如果批量修改多个css属性时，使用style一次只能改一个css属性。代码会很繁琐。  
解决办法: __只要批量修改元素的样式都要先将多个css属性定义为一个class，再用.className="class名"一句话批量应用。__
