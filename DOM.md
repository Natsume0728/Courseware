# DOM HTML_DOM常用对象 BOM

- [DOM](#dom)  
  - [查找元素](#查找元素(4种方法))  
  - [修改](#修改(3种方法))  
  - [添加/删除](#添加/删除)  
- [HTML_DOM常用对象](#html_dom常用对象)  
  - [Image对象](#_image对象)
  - [Select对象](#select对象)
  - [Option对象](#option对象)
  - [Table对象](#table对象)
  - [Form对象](#form对象)
- [BOM](#bom)
  - [window](#window(充当了3个角色))
  - [打开窗口](#打开窗口(4种方法))
  - [window.history](#window.history)
  - [window.location](#window.location)
  - [window.navigator](#window.navigator)

## DOM  

<blockquote>DOM<br>  
专门操作网页内容的一套对象和函数的集合,<br>
只要操作网页的内容都用DOM,<br>
DOM其实是一套对象和函数的标准——W3C制定,<br>
统一了所有浏览器开发网页内容的标准,几乎所有浏览器100%兼容DOM标准。
<blockquote>DOM 树<br>  
内存中，保存当前网页中所有内容的树形结构<br>
树形结构是最直观的存储上下级包含关系的结构。<br>  
而网页中的所有元素内容，都是上下级包含关系的。  
<blockquote>DOM树长什么样？<br>
当浏览器读到网页时，先在内存中创建网页的根节点对象: documen<br>
浏览器按从上到下的顺序读取网页内容，每读到一项网页内容，就创建一个节点对象，并挂到指定父节点下。
</blockquote></blockquote></blockquote>

ECMAScript|DOM|BOM
:---:|:---:|:---:
核心语法 | 操作网页内容 | 操作浏览器窗口
ES标准 | W3C标准 | 没有标准

### 查找元素(4种方法)

#### 1. 不需要查找就可以直接获得的元素

- document:    根节点对象
- \<html>根元素:    document.documentElement
- \<head>元素:    document.head
- \<body>元素:    document.body

#### 2. 按节点间关系查找  

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

#### 3. 按HTML特征查找

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

#### 4. 按任意选择器查找元素

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

### 修改(3种方法)

#### 1. 内容

1. 获取或设置元素开始标签到结束标签之间的原始HTML代码片段: 元素.innerHTML  
1. 获取或设置元素开始标签到结束标签之间的纯文本内容: 元素.textContent  
   和innerHTML比较:
   1. 去掉了内嵌的标签
   2. 转义符号翻译为正文
1. 获取或设置表单元素的值:表单元素.value

#### 2. 属性(3大类)

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

#### 3. 样式

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

### 添加/删除

#### 添加一个新元素(3步)

1. 先创建一个空元素:
var a=document.createElement("标签名")  
结果: \<a>\</a>
2. 设置空元素的关键属性:  
a.href="<http://tmooc.cn">  
a.innerHTML="go to tmooc";  
结果:\<a href="<http://tmooc.cn">go> to tmooc\</a>
3. 将新元素挂载到DOM树上的指定位置上:
   1. 在指定父元素末尾追加子元素  
父元素.appendChild(新元素)  
比如:`body.appendChild(a)`将a元素追加到body元素下子元素的末尾  
   2. 插入到现有一个元素之前  
父元素.insertBefore(新元素, 现有元素)  
比如:`body.insertBefore(a, h1)`将a插入到h1之前
   3. 替换现有的一个元素  
父元素.replaceChild(新元素, 现有元素)  
比如:`body.replaceChild(a, h1)`用a替换body下的h1  

         __优化:尽量减少操作DOM树的次数__  
         WHY:每操作一次DOM树，浏览器都要重绘整个页面，效率很低！会造成闪屏  
         HOW:2种方式
      1. 如果同时添加父元素和子元素时，应该先在内存中将所有子元素添加到父元素中。最后再一次性将父元素整体添加到DOM树——只重绘一次
      2. 如果父元素已经在页面上了，要添加多个平级子元素。  
借助文档片段:  
什么是: 内存中临时保存多个平级子元素的虚拟父元素  
何时: 如果父元素已经在页面上了，要添加多个平级子元素  
 如何: 3步  
             1. 临时创建文档片段托盘对象:  
      `var frag=document.createDocumentFragment();`  
             2. 将子元素临时添加到文档片段对象中:  
      `frag.appendChild(子元素)`  
             3. 将文档片段添加到页面中指定的父元素下  
      `父元素.appendChild(frag)`  
      结果: frag将子元素都送到父元素指定位置后，就释放了！不占用页面空间。

#### 删除

任意父元素.removeChild(孩子)  
或者:  
孩子.parentNode.removeChild(孩子)

## HTML DOM常用对象

>HTML DOM是对原有DOM函数和对象的简化
HTML DOM 对一些常用的元素对象也提供了简化的函数和属性
比如: \<img> \<select>\<option>  \<table>...\</table>  \<form>...  

### Image对象

>就是一个\<img>元素  

 唯一的简化，就是在创建\<img>元素时:  
 `var img=new Image();`  
 __强调:__ 通常只要两个元素可以用new简写: \<img> \<option>  
 其它元素依然需要document.createElement()创建  

### Select对象

>就是一个\<select>元素  

简化:  

- 属性:  
    .selectedIndex  获得select下选中的option的下标位置  
    .options 获得select下所有option元素的集合  
    .options.length 获得select下所有option元素的个数  
    .length <==> .options.length  
- 方法:  
    .add(option) <==> .appendChild(option) 追加一个option  
    问题:  
    .add( )不支持frag  
    .appendChild( )支持frag  
    .remove(i) 移除i位置的一个option  

### Option对象

>就是一个option元素

&nbsp;&nbsp; &nbsp;唯一的简化，就是在创建时:  
&nbsp;&nbsp; &nbsp;`var option=new Option(内容文本, value)`  
&nbsp;&nbsp; &nbsp;比如: var option=new Option("-请选择-",0)  
&nbsp;&nbsp; &nbsp;结果: \<option value="0">-请选择-\</option>  
&nbsp;&nbsp; &nbsp;vs 原DOM函数:  
&nbsp;&nbsp; &nbsp;`var option=document.createElement("option")`  
&nbsp;&nbsp; &nbsp;`option.value=0;`  
&nbsp;&nbsp; &nbsp;`option.innerHTML="-请选择-"`  

### Table对象

>代表页面上一个\<table>元素

- Table对象直接管着行分组:  

  - 创建行分组: table.createTHead()
             table.createTBody()
             table.createTFoot()
  - 删除行分组: table.deleteTHead()
             table.deleteTFoot()
  - 获得行分组:__table.tHead__
              __table.tFoot__
              __table.tBodies[i]__

- 行分组管着行:  

  - 创建行:  
  var tr=tbody.insertRow(i)  
  在tbody中第i行位置插入一个新行,并返回刚添加的新行对象，便于后续对新 行中添加格和数据。  
  __强调:insertRow()不但创建新行，而且立刻将新行添加到tbody中__。  
  vs 原DOM: 2步:  
  var tr=document.createElement("tr")  
  tbody.appendChild(tr)  
  __固定套路:__  
    - __在tbody开头插入一个新行__  
    var tr=tbody.insertRow(0)
    - __在tbody结尾追加一个新行__  
    var tr=tbody.insertRow( )
  - 删除行:  
  tbody.deleteRow(i) 删除tbody中i位置的行  
  问题:  
  __i 要求是行在tbody内部的相对下标位置,而一个tr对象的相对下标位置无法  自动获得,可以自动获得的tr.rowIndex是相对于整个表中的下标位置。和  tbody.deleteRow()的要求错位。__  
  解决:  
  __只要删除行的标准写法都是: table.deleteRow(tr.rowIndex)  
  因为.前的主语变成整个table，所以deleteRow( )要求就变为使用整个表中  的下标，就和tr.rowIndex的意义相符了。__
  - 获取行: tbody.rows[i]  

- 行管着格:  
  - 添加格:  
    var td=tr.insertCell(i)  
    __通常都是在行末尾追加一格:var td=tr.insertCell()__  
    VS 旧DOM:  
    var td=document.createElement("td");  
    tr.appendChild(td);  
  - 删除格: tr.deleteCell(i)
  - 获取格: tr.cells[i]

### Form对象

>代表一个\<form>元素

获取表单对象: 其实也不需要查找，就可直接获得。  
因为表单对于所在的网页极其重要，所以网页就将本页面内的\<form>元素都保存在一个forms集合中。  
可用[i]获取某一个表单对象 var form = document.forms[i]  
比如:  
如果一个页面中只有一个\<form> 则 var form=document.forms[0]  

- 属性:  
    form.elements  获得表单中所有表单元素的集合.  
    form.elements.length 获得表单中所有表单元素的个数.  
    form.length <==> form.elements.length
表单元素对象:  比如: \<input>  \<select>  \<textarea> \<button>  
   获取表单中的表单元素:  

  - 普通方法: var 表单元素=form.elements[id|i|name]  
    比如:  
    - 获得form中name=username的input元素  
        var txtName=form.elements["username"]  
    - 获得form中的倒数第二个表单元素——input type=button保存按钮  
        var btnSubmit=form.elements[form.length-2];  
  - 简写: 如果一个表单元素有name属性，可直接用.name方法获得:  
        var txtName=form.elements["username"]  
           可简写为: form.username;  
- 方法: 表单元素.focus() 让当前表单元素自动获得焦点  

## BOM

>Browser Object Model:操作浏览器窗口的对象和函数  

ECMAScript|DOM|BOM
:---:|:---:|:---:
核心语法 | 操作网页内容 | 操作浏览器窗口
ES标准 | W3C标准 | 没有标准
问题: 没有标准——极大的兼容性问题，所以用的越来越少  

### window(充当了3个角色)

1. 顶替了ES标准中的global，充当全局作用域对象  
比如:  
浏览器中: var a=10;  window.a 输出10  
再比如:  
      window.parseInt()  
      window.parseFloat()  
      window.Array  
      window.Date  
      window.RegExp  
2. 包含所有ES,DOM,BOM的对象和函数  
 比如:  
 window.document  
 window.document.getElementById( )  
3. 还代表当前正在打开的窗口  
   比如:  
   window.close( ) 是关闭当前窗口的意思  
   新chrome浏览器禁止随意关闭窗口，弹出黄色警告  
   再比如:  
   window.outerWidth 可获得当前窗口的总宽度  
   window.outerHeight 可获得当前窗口的总高度 

### 打开窗口(4种方法)  

  1. 在当前窗口打开新链接，可后退  
    html: \<a href="url" target="_self">  
    js: window.open("url","_self")  
  2. 在当前窗口打开新链接，禁止后退(在一个窗口内，反复打开多个链接时才能实现)  
    js: location.replace("新url")  
    原理: 用新的url地址，替换history中旧的地址，保证history中只有一条url，以此禁止后退  
  3. 在新窗口打开新链接，可同时打开多个  
    html: \<a href="url" target="_blank">  
    js: window.open("url","_blank")  
  4. 在新窗口打开新链接，只能打开一个  
    html: \<a href="url" target="自定义新窗口名">  
    js: window.open("url","自定义新窗口名")  
    原理: 其实，每个窗口在浏览器内存中都有一个唯一的名字，用来标识这个窗口。  
    浏览器规定，相同名称的窗口，只能打开一个。  
    新打开的同名窗口会覆盖现有的重名窗口  
    tips:  
    如果打开链接时，使用自定义窗口名，则反复点击链接，只能打开一个  
    有两个预定义窗口名:  
    _self: 自动获取当前窗口自己的名字给新窗口  
    结果: 新窗口会覆盖当前窗口  
    _blank: 空白，就是不指定新窗口名，浏览器会自动在底层分配，保证不重复。  
    结果: 不限制打开的新窗口个数  

### window.history

>保存当前窗口打开后，成功访问过的url的历史记录数组

当前窗口只要成功访问过一个url，url就会被push到history中保存。  
能否前进后退，取决于现在正在看的url，在history前后是否有其他已经浏览过的url  
只开放了一个函数: history.go(i)  
比如:  

- 前进一步: history.go(1)
- 后退一步: history.go(-1)
- 刷新: history.go(0)
- 后退两步: history.go(-2)

### window.location

>专门保存地址栏中url信息的对象，并提供了打开新链接的方法

- 属性:  
 可分段获得url的各个组成部分(协议 主机/IP 端口 相对路径):  
  完整url: location.href  
  <http://127.0.0.1:5500/BOM/10_location.html?username=dingding&pwd=123456&favs=running#top>  
  协议: location.protocol  
  主机+端口: location.host  
  主机: location.hostname  
  端口: location.port  
  相对路径: location.pathname  
  查询字符串: location.search  
   ?username=dingding&pwd=123456&favs=running  
  锚点地址: location.hash  #top
- 方法:  
  1. 在当前窗口打开新链接，可后退: location.href="新url"
  2. 在当前窗口打开新链接，禁止后退:  
     location.replace("新url")
  3. 刷新: location.reload();

### window.navigator

>保存浏览器配置信息的对象  

__鄙视题:__ 如何判断正在使用的浏览器的名称和版本号?  
userAgent: 保存浏览器名称和版本号的字符串  
