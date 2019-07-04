# DOM &nbsp; HTML DOM 常用对象 &nbsp; BOM

<!-- TOC depthFrom:2 orderedList:false -->

- [DOM](#dom)
    - [查找元素](#查找元素)
        - [1. 不需要查找就可以直接获得的元素](#1-不需要查找就可以直接获得的元素)
        - [2. 按节点间关系查找](#2-按节点间关系查找)
        - [3. 按 HTML 特征查找](#3-按-html-特征查找)
        - [4. 按任意选择器查找元素](#4-按任意选择器查找元素)
    - [修改](#修改)
        - [1. 内容](#1-内容)
        - [2. 属性(3 大类)](#2-属性3-大类)
        - [3. 样式](#3-样式)
    - [添加和删除](#添加和删除)
        - [添加一个新元素(3 步)](#添加一个新元素3-步)
        - [删除](#删除)
- [HTML DOM 常用对象](#html-dom-常用对象)
    - [Image 对象](#image-对象)
    - [Select 对象](#select-对象)
    - [Option 对象](#option-对象)
    - [Table 对象](#table-对象)
    - [Form 对象](#form-对象)
- [事件](#事件)
    - [绑定事件处理函数](#绑定事件处理函数)
    - [事件模型](#事件模型)
    - [事件对象](#事件对象)
- [BOM](#bom)
    - [window](#window)
    - [打开窗口](#打开窗口)
    - [history](#history)
    - [location](#location)
    - [navigator](#navigator)

<!-- /TOC -->

<!-- - [DOM](#dom)
  - [查找元素](#查找元素)
  - [修改](#修改)
  - [添加/删除](#添加和删除)
- [HTML DOM 常用对象](#html-dom-常用对象)
  - [Image 对象](#image-对象)
  - [Select 对象](#select-对象)
  - [Option 对象](#option-对象)
  - [Table 对象](#table-对象)
  - [Form 对象](#form-对象)
- [事件](#事件)
  - [绑定事件处理函数](#绑定事件处理函数)
  - [事件模型](#事件模型)
  - [事件对象](#事件对象)
- [BOM](#bom)
  - [window](#window)
  - [打开窗口](#打开窗口)
  - [window.history](#history)
  - [window.location](#location)
  - [window.navigator](#navigator) -->

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

| ECMAScript |     DOM      |      BOM       |
| :--------: | :----------: | :------------: |
|  核心语法  | 操作网页内容 | 操作浏览器窗口 |
|  ES 标准   |   W3C 标准   |    没有标准    |

### 查找元素

> 有 4 中查找元素的方法

#### 1. 不需要查找就可以直接获得的元素

- document: 根节点对象
- \<html>根元素: document.documentElement
- \<head>元素: document.head
- \<body>元素: document.body

#### 2. 按节点间关系查找

何时：如果已经获得一个节点对象，找周围附近的节点对象时  
节点树：包含 **所有网页内容** 的完整树结构  
包括：2 大类关系

1. 父子关系：4 个属性
   - 节点.parentNode
   - 节点.childNodes
     返回多个直接子节点组成的 **类数组对象** 可用下标访问指定位置的子节点。
   - 节点.firstChild
   - 节点.lastChild
1. 兄弟关系：2 个属性
   - 元素.previousElementSibling
   - 元素.nextElementSibling  
     节点树的缺陷：节点树包含了所有节点，包括看不见的空字符节点。给查找元素造成了极大的障碍。程序员只关心元素节点，不关心文字节点。

解决:  
元素树: 仅包含元素节点的树结构  
包括: 2 大类关系

1. 父子关系: 4 个属性
   - 元素.parentElement
   - 元素.children  
      返回多个直接子元素组成的类数组对象，可用下标访问指定位置的子元素
   - 元素.firstElementChild
   - 元素.lastElementChild
1. 兄弟关系: 2 个属性
   - 元素.previousElementSibling
   - 元素.nextElementSibling  
     **元素树的优点**：不包含看不见的空字符，不会受到空字符的干扰。

**鄙视题**：遍历一个指定元素下的所有后代元素，找到符合条件的元素。

```html
<script>
  var uname = "dingding";
  var title = "极限挑战";
  function fun(parent) {
    for (let elem of parent.children) {
      if (elem.innerHTML == "{{uname}}") {
        elem.innerHTML = uname;
      }
      if (elem.innerHTML == "{{title}}") {
        elem.innerHTML = title;
      }
      arguments.callee(elem);
      // fun(elem)
    }
  }
  fun(document.body);
</script>
```

#### 3. 按 HTML 特征查找

按节点间关系查找的缺点：必须先有一个节点，才能找周围的关系。  
解决办法：在还未获得元素的情况下，执行首次查找，用按 HTML 特征查找。

1. 按 id 查找一个元素
   var elem = document.getElementById('id 值')  
   **强调:**
   1. 必须用 document 调用。
   2. 只能找到一个符合条件的元素，如果有两个 id 相同，只能找到第一个。
1. 按标签名查找多个元素
   var elem = 任意父元素.getElementsByTagName('标签名')  
   **强调:**
   1. 可以用任意父元素调用，用哪个父元素调用，就只在哪个父元素下查找
   2. 返回对个元素组成的类数组对象
   3. 不仅查找直接子元素，且查找所有后代
1. 按 class 名查找多个元素  
   var elem = 任意父元素.getElementByClassName('class 名')  
   **强调:**
   1. 用任意父元素调用
   2. 返回多个元素组成的类数组对象
   3. 不仅查找直接子元素，且查找所有后代
   4. 仅靠其中一个 class，就可以找到元素
1. 按 name 属性值查找多个元素  
   var elem = document.getElementByName('name 值')  
   专门用于查找表单中有 name 属性的表单元素  
   **强调:**
   1. 只能用 document 调用
   2. 返回多个元素组成的类数组对象

#### 4. 按任意选择器查找元素

1. 仅查找一个符合条件的元素:  
   var elem=任意父元素.querySelector("选择器")  
   **强调:**
   1. 用任意父元素调用  
      如果采用指定父元素，调用函数时必须是相对于父元素内的相对选择器  
      比如:  
      `document.querySelector("table>tbody td:last-child ")`  
      `table.querySelector("tbody td:last-child")`  
      ~~`table.querySelector("table>tbody td:last-child ")`~~
   2. 只能返回 1 个元素
   3. 不仅查找直接子元素，且在所有后代中查找
2. 查找所有符合条件的元素:  
   var elems=任意父元素.querySelectorAll("任意选择器")  
   **强调:**
   1. 用任意父元素调用，缩小范围
   2. 可返回所有符合条件的元素的类数组对象
   3. 不仅查找直接子元素，且在所有后代中查找

缺点: **用选择器查找，效率不如用 HTML 特征查找高**。

**总结:**

1. 如果只要一个条件，就能找到想要的元素时，首选按 HTML 特征查找
2. 如果查找条件复杂时，需要多个条件才能找到想要的元素时，就首选按选择器查找——简单！

---

### 修改

> 有 3 种修改的方式

#### 1. 内容

1. 获取或设置元素开始标签到结束标签之间的原始 HTML 代码片段: 元素.innerHTML
1. 获取或设置元素开始标签到结束标签之间的纯文本内容: 元素.textContent  
   和 innerHTML 比较:
   1. 去掉了内嵌的标签
   2. 转义符号翻译为正文
1. 获取或设置表单元素的值:  
   表单元素.value

#### 2. 属性(3 大类)

1. HTML 标准属性: HTML 标准中规定的属性  
   比如: title, class, href, src, target, id  
   2 种:

   1. 用最初的核心 DOM 函数(4 个):  
      var 属性值=元素.getAttribute("属性名");  
      元素.setAttribute("属性名","属性值");  
      var bool=元素.hasAttribute("属性名")  
      元素.removeAttribute("属性名")
   1. HTML DOM——核心 DOM 函数的简化版  
      将所有的 HTML 标准属性都提前定义在了元素对象上，属性值暂时都是""。  
      元素.属性  
      比如:
      - 获得属性值: 元素.属性
      - 修改属性值: 元素.属性=值
      - 判断是否包含属性: 元素.属性!==""
      - 移除属性: 元素.属性=""  
        **总结:**  
        今后只要是 HTML 标准属性，都可用.访问  
        **特例:** class 属性，虽然是标准属性，但不能直接用.访问  
         class 是 js 的关键词。  
        **解决办法:** 今后，凡是使用 class 属性，一律更名为 className,使用 className 等于使用 class。

1. 状态属性: disabled &nbsp; checked &nbsp; selected  
   特殊: 他们的值都是 bool 类型  
   而核心 DOM 的 4 个函数只能操作字符串类型的标准属性  
   所以，**状态属性只能用.访问！**
1. 自定义扩展属性:HTML 标准中没有规定的，程序员自发添加的属性  
   2 个典型使用场景:
   1. 在客户端临时缓存数据，减少向服务器端发送请求的次数
   2. 代替其它选择器，用于选择触发事件的元素，绑定事件处理函数
      如何使用自定义扩展属性:
      1. 添加自定义扩展属性:
      - 在 html 页面中写死: <ANY data-自定义属性名="值"  
        比如:\<img src="1.png" data-m="m.png" data-l="l.png">
      - 用程序动态设置: 只能用 setAttribute，不能用.  
        比如: img.setAttribute("data-m","m.png")  
        结果:\<img data-m="m.png"> 2. 修改自定义扩展属性: 也只能用 setAttribute()
   3. 读取自定义扩展属性的值: 只能用 getAttribute()
      - 比如: var m=img.getAttribute("data-m") &nbsp;m="m.png"  
        **强调:** 因为自定义扩展属性，只出现在页面中，不在内存中，  
        所以，只能用 getAttribute()&nbsp; setAttribute()...来访问，不能用.访问。

#### 3. 样式

修改内联样式: 元素.style.css 属性="值"

- 比如: div.style.display="block">  
  效果: \<div style="display:block">  
  **强调:**

1. css 属性名如果带-，要去横线变驼峰  
   比如:
   - z-index -> zIndex
   - background-position -> backgroundPosition
1. 如果 css 属性值带单位，则必须加单位！  
   问题: 如果批量修改多个 css 属性时，使用 style 一次只能改一个 css 属性。代码会很繁琐。  
   解决办法: **只要批量修改元素的样式都要先将多个 css 属性定义为一个 class，再用.className="class 名"一句话批量应用。**

### 添加和删除

#### 添加一个新元素(3 步)

1. 先创建一个空元素:
   var a=document.createElement("标签名")  
   结果: \<a>\</a>
2. 设置空元素的关键属性:  
   a.href=`"http://tmooc.cn"`  
   a.innerHTML="go to tmooc";  
   结果:\<a href=`"http://tmooc.cn"`>go to tmooc\</a>
3. 将新元素挂载到 DOM 树上的指定位置上:

   1. 在指定父元素末尾追加子元素  
      父元素.appendChild(新元素)  
      比如:`body.appendChild(a)`将 a 元素追加到 body 元素下子元素的末尾
   2. 插入到现有一个元素之前  
      父元素.insertBefore(新元素, 现有元素)  
      比如:`body.insertBefore(a, h1)`将 a 插入到 h1 之前
   3. 替换现有的一个元素  
      父元素.replaceChild(新元素, 现有元素)  
      比如:`body.replaceChild(a, h1)`用 a 替换 body 下的 h1

**优化:尽量减少操作 DOM 树的次数**  
 WHY:每操作一次 DOM 树，浏览器都要重绘整个页面，效率很低！会造成闪屏  
HOW:2 种方式

1. 如果同时添加父元素和子元素时，应该先在内存中将所有子元素添加到父元素中。  
   最后再一次性将父元素整体添加到 DOM 树——只重绘一次
2. 如果父元素已经在页面上了，要添加多个平级子元素。  
   借助 **文档片段**:  
    什么是: 内存中临时保存多个平级子元素的虚拟父元素  
    何时: 如果父元素已经在页面上了，要添加多个平级子元素  
    如何: 3 步
   1. 临时创建文档片段托盘对象:  
      `var frag=document.createDocumentFragment();`
   2. 将子元素临时添加到文档片段对象中:  
      `frag.appendChild(子元素)`
   3. 将文档片段添加到页面中指定的父元素下  
      `父元素.appendChild(frag)`  
      结果: frag 将子元素都送到父元素指定位置后，就释放了！不占用页面空间。

#### 删除

任意父元素.removeChild(孩子)  
或者:  
孩子.parentNode.removeChild(孩子)

## HTML DOM 常用对象

> HTML DOM 是对原有 DOM 函数和对象的简化
> HTML DOM 对一些常用的元素对象也提供了简化的函数和属性
> 比如: \<img> \<select>\<option> \<table>...\</table> \<form>...

### Image 对象

> 就是一个\<img>元素

唯一的简化，就是在创建\<img>元素时:  
 `var img=new Image();`  
 **强调:** 通常只要两个元素可以用 new 简写: \<img> \<option>  
 其它元素依然需要 document.createElement()创建

### Select 对象

> 就是一个\<select>元素

简化:

- 属性:  
   .selectedIndex 获得 select 下选中的 option 的下标位置  
   .options 获得 select 下所有 option 元素的集合  
   .options.length 获得 select 下所有 option 元素的个数  
   .length <==> .options.length
- 方法:  
   .add(option) <==> .appendChild(option) 追加一个 option  
   问题:  
   .add( )不支持 frag  
   .appendChild( )支持 frag  
   .remove(i) 移除 i 位置的一个 option

### Option 对象

> 就是一个 option 元素

&nbsp;&nbsp; &nbsp;唯一的简化，就是在创建时:  
&nbsp;&nbsp; &nbsp;`var option=new Option(内容文本, value)`  
&nbsp;&nbsp; &nbsp;比如: var option=new Option("-请选择-",0)  
&nbsp;&nbsp; &nbsp;结果: \<option value="0">-请选择-\</option>  
&nbsp;&nbsp; &nbsp;vs 原 DOM 函数:  
&nbsp;&nbsp; &nbsp;`var option=document.createElement("option")`  
&nbsp;&nbsp; &nbsp;`option.value=0;`  
&nbsp;&nbsp; &nbsp;`option.innerHTML="-请选择-"`

### Table 对象

> 代表页面上一个\<table>元素

- Table 对象直接管着行分组:
  - 创建行分组:  
     table.createTHead()  
     table.createTBody()  
     table.createTFoot()
  - 删除行分组:  
    table.deleteTHead()  
    table.deleteTFoot()
  - 获得行分组:  
    **table.tHead**  
    **table.tFoot**  
    **table.tBodies[i]**
- 行分组管着行:

  - 创建行:  
    var tr=tbody.insertRow(i)  
    在 tbody 中第 i 行位置插入一个新行,并返回刚添加的新行对象，便于后续对新 行中添加格和数据。  
    **强调:insertRow()不但创建新行，而且立刻将新行添加到 tbody 中**。  
    vs 原 DOM: 2 步:  
    var tr=document.createElement("tr")  
    tbody.appendChild(tr)  
    **固定套路:**
    - **在 tbody 开头插入一个新行**  
      var tr=tbody.insertRow(0)
    - **在 tbody 结尾追加一个新行**  
      var tr=tbody.insertRow( )
  - 删除行:  
    tbody.deleteRow(i) 删除 tbody 中 i 位置的行  
    问题:  
    **i 要求是行在 tbody 内部的相对下标位置,  
    而一个 tr 对象的相对下标位置无法自动获得,  
    可以自动获得的 tr.rowIndex 是相对于整个表中的下标位置。
    和 tbody.deleteRow()的要求错位。**  
    解决:  
    **只要删除行的标准写法都是: table.deleteRow(tr.rowIndex)  
    因为.前的主语变成整个 table，所以 deleteRow( )要求就变为使用整个表中 的下标，就和 tr.rowIndex 的意义相符了。**
  - 获取行: tbody.rows[i]

- 行管着格:
  - 添加格:  
    var td=tr.insertCell(i)  
    **通常都是在行末尾追加一格:var td=tr.insertCell()**  
    VS 旧 DOM:  
    var td=document.createElement("td");  
    tr.appendChild(td);
  - 删除格: tr.deleteCell(i)
  - 获取格: tr.cells[i]

### Form 对象

> 代表一个\<form>元素

获取表单对象: 其实也不需要查找，就可直接获得。  
因为表单对于所在的网页极其重要，所以网页就将本页面内的\<form>元素都保存在一个 forms 集合中。  
可用[i]获取某一个表单对象 var form = document.forms[i]  
比如:  
如果一个页面中只有一个\<form> 则 var form=document.forms[0]

- 属性:  
   form.elements 获得表单中所有表单元素的集合.  
   form.elements.length 获得表单中所有表单元素的个数.  
   form.length <==> form.elements.length  
  表单元素对象: 比如: \<input> \<select> \<textarea> \<button>  
   获取表单中的表单元素:

  - 普通方法: var 表单元素=form.elements[id / i / name]  
    比如:
    - 获得 form 中 name=username 的 input 元素  
       var txtName=form.elements["username"]
    - 获得 form 中的倒数第二个表单元素——input type=button 保存按钮  
       var btnSubmit=form.elements[form.length-2];
  - 简写: 如果一个表单元素有 name 属性，可直接用.name 方法获得:  
     var txtName=form.elements["username"]  
     可简写为: form.username;

- 方法: 表单元素.focus() 让当前表单元素自动获得焦点

---

## 事件

> 浏览器自动触发的或用户手动触发的页面内容、状态的改变.

**事件处理函数:** 当事件发生时自动调用的函数.  
**强调: 事件处理函数中的 this 永远指当前触发事件的元素**

### 绑定事件处理函数

每个元素对象上都有一批 on 开头的特殊属性，这些属性会在事件发生时自动触发对应的属性。  
如果希望事件发生时，按照我们的意愿执行操作，就要提前将一个自定义函数赋值给 on 开头的对应属性保存起来,当事件发生时，会自动调用提前保存的函数。  
**如何绑定:**

- 在 HTML 中:  
  `\<ANY onclick="js语句/函数调用">...\<ANY>`  
  `function 事件处理函数( ){ ... }`  
  问题: 不符合内容与行为分离的原则，不便于维护和重用
- 在 js 中用赋值方式:  
  `元素对象.onclick=function(){`  
  `... this 指当前触发事件的元素对象`  
  `}`  
  问题: 一个事件只能绑定一个处理函数，不灵活！
- 在 js 中用添加事件监听对象的方式:  
   `元素对象.addEventListener("事件名",处理函数)`  
   **强调: 真正的事件名是没有 on 前缀的**  
   **比如: click &#160; change &#160; focus &#160; blur &#160; load**  
   比如:  
  `btnShoot.addEventListener("click",function(){发射普通子弹})`  
  `btnShoot.addEventListener("click",function(){发射跟踪导弹})`  
  结果: 单击 btnShoot，会先后发射两种子弹

原理:

> 其实，浏览器中有一个巨大的事件监听队列，  
> 我们为每个元素绑定的事件监听对象都会被添加到监听队列中；  
> 当事件发生时，浏览器采用遍历监听队列的方式，找到符合条件的事件监听对象，并执行其中的处理函数，  
> 找到几个符合条件的，就执行几个符合条件的。

**移除事件监听对象:**  
`元素对象.removeEventListener("事件名", 处理函数)`  
**强调: 移除监听对象时，元素、事件名和处理函数都要和添加时完全相同！**  
**坑: 如果一个处理函数可能被移除，则添加监听时，就要使用有名称的函数。不能使用匿名函数**

### 事件模型

> 从触发事件开始，到所有事件处理函数执行完，所经历的过程,包括三个阶段:

1. 捕获: 由外(document)向内(实际触发事件的元素)记录各级父元素上绑定的相同事件的处理函数,**只记录，不执行**。
1. 目标触发: 优先触发目标元素上的处理函数  
   目标(target)元素: 最初实际触发事件的那个元素
1. **冒泡: 由内向外，依次触发各级父元素上收集的相同事件的处理函数**。

### 事件对象

> 在事件发生时，浏览器自动创建的，收集事件相关信息的对象。并提供了改造事件的函数.

2 种使用场景：

- 想获得事件信息时: 点了那个元素，点在什么位置...
- 想改造事件默认的行为:**取消冒泡！**  
  如何:

  1. 获取: 不用自己创建  
     事件对象总是作为处理函数的第一个实参默认传入！  
     我们只要在定义处理函数时，提前定义一个形参接住  
     比如:  
     btn.onclick=function(e){  
      //当事件发生时: e 自动收到浏览器给的 event 对象  
      }  
      btn.addEventListener("click",function(e){ ... })
  2. 包括哪些功能?

     - **取消冒泡: e.stopPropagation()**  
       什么是: 当前元素处理函数执行完，停止继续执行父元素上的处理函数。  
       何时: 只要不希望触发父元素上的处理函数时，都要取消冒泡。
     - **事件委托/事件代理:**  
       优化:  
       尽量减少事件监听的个数。  
       为什么:  
       浏览器触发事件，是采用遍历监听数组中每个监听对象来匹配并触发处理函数的。  
       数组中监听对象多，遍历速度慢，数组中监听对象少，遍历快！  
       何时:  
       多个平级子元素，要绑定相同的事件处理函数时，只要在父元素绑定一次即可。  
       如何:  
       只要在父元素上统一绑定一次事件处理函数即可。  
       点击子元素时，会自动冒泡到父元素上，执行提前委托好的处理函数。  
       **坑 1: 如何获得最初触发事件的目标元素？**  
        错误:使用 this  
        因为事件绑在父元素上，执行时，也是冒泡到父元素才执行的。所以，**事件委托中的 this 一律指父元素。**  
        正确:**e.target 记录了事件最初触发的目标元素,不随冒泡而改变**  
        坑 2:**所有点击的元素都是想要的吗？不是!**  
        **在正式执行逻辑前，都要先判断目标元素是否是想要的。**  
        **哪些属性可作为区分的条件:(节点名，标签名) nodeName, className,...**  
        **nodeName 节点名 返回的节点名为全大写 如：BUTTON**  
     - **阻止默认行为: 有些元素自带默认行为。**  
       何时: 如果元素自带的默认行为不是我们想要的，就可用 **e.preventDefault( )** 来阻止默认行为的发生  
       比如: bootstrap 中,\<a href="#content1" data-toggle="tab">  
       点 a 时，不但执行绑定的操作，还会附加修改地址栏中的 url(后加#content1 锚点地址)  
       所以，**只要用 a 当做普通按钮用时，都要阻止默认行为。**

     - **鼠标坐标: 事件对象在事件发生时，就自动获得了鼠标在屏幕中的位置。**  
       包括 3 组:
       1. 相对于屏幕左上角: e.screenX &#160; e.screenY
       2. 相对于浏览器文档显示区左上角: e.clientX &#160; e.clientY
       3. 相对于当前元素左上角: e.offsetX &#160; e.offsetY

---

## BOM

> Browser Object Model:操作浏览器窗口的对象和函数

| ECMAScript |     DOM      |      BOM       |
| :--------: | :----------: | :------------: |
|  核心语法  | 操作网页内容 | 操作浏览器窗口 |
|  ES 标准   |   W3C 标准   |    没有标准    |

问题: 没有标准——极大的兼容性问题，所以用的越来越少

### window

> 充当了 3 个角色

1. 顶替了 ES 标准中的 global，充当全局作用域对象  
   比如:  
   浏览器中: var a=10; window.a 输出 10  
   再比如:  
    window.parseInt()  
    window.parseFloat()  
    window.Array  
    window.Date  
    window.RegExp
2. 包含所有 ES,DOM,BOM 的对象和函数  
   比如:  
   window.document  
   window.document.getElementById( )
3. 还代表当前正在打开的窗口  
   比如:  
   window.close( ) 是关闭当前窗口的意思  
   新 chrome 浏览器禁止随意关闭窗口，弹出黄色警告  
   再比如:  
   window.outerWidth 可获得当前窗口的总宽度  
   window.outerHeight 可获得当前窗口的总高度

### 打开窗口

> 打开窗口的方式有 4 种

1. 在当前窗口打开新链接，可后退  
   html: \<a href="url" target="\_self">  
   js: window.open("url","\_self")
2. **在当前窗口打开新链接，禁止后退**(在一个窗口内，反复打开多个链接时才能实现)  
   js: location.replace("新 url")  
   原理: 用新的 url 地址，替换 history 中旧的地址，保证 history 中只有一条 url，以此禁止后退
3. 在新窗口打开新链接，可同时打开多个  
   html: \<a href="url" target="\_blank">  
   js: window.open("url","\_blank")
4. 在新窗口打开新链接，只能打开一个  
   html: \<a href="url" target="自定义新窗口名">  
   js: window.open("url","自定义新窗口名")  
   原理: 其实，每个窗口在浏览器内存中都有一个唯一的名字，用来标识这个窗口。  
   浏览器规定，相同名称的窗口，只能打开一个。  
   新打开的同名窗口会覆盖现有的重名窗口

   tips:  
   如果打开链接时，使用自定义窗口名，则反复点击链接，只能打开一个  
   **有两个预定义窗口名**:  
   \_self: 自动获取当前窗口自己的名字给新窗口  
   结果: 新窗口会覆盖当前窗口  
   \_blank: 空白，就是不指定新窗口名，浏览器会自动在底层分配，保证不重复。  
   结果: 不限制打开的新窗口个数

### history

> window.history 保存当前窗口打开后，成功访问过的 url 的历史记录数组

当前窗口只要成功访问过一个 url，url 就会被 push 到 history 中保存。  
能否前进后退，取决于现在正在看的 url，在 history 前后是否有其他已经浏览过的 url  
只开放了一个函数: history.go(i)  
比如:

- 前进一步: history.go(1)
- 后退一步: history.go(-1)
- 刷新: history.go(0)
- 后退两步: history.go(-2)

### location

> window.location 专门保存地址栏中 url 信息的对象，并提供了打开新链接的方法

- 属性:  
  可分段获得 url 的各个组成部分(协议 主机/IP 端口 相对路径):  
   完整 url: location.href  
   `<http://127.0.0.1:5500/BOM/10_location.html?username=dingding&pwd=123456&favs=running#top>`<br>
  协议: location.protocol  
   主机+端口: location.host  
   主机: location.hostname  
   端口: location.port  
   相对路径: location.pathname  
   查询字符串: location.search  
   ?username=dingding&pwd=123456&favs=running  
   锚点地址: location.hash  
   #top
- 方法:
  1. 在当前窗口打开新链接，可后退:  
     location.href="新 url"
  2. 在当前窗口打开新链接，禁止后退:  
     location.replace("新 url")
  3. 刷新:  
     location.reload();

### navigator

> window.navigator 保存浏览器配置信息的对象  
> userAgent:用户代理字符串，保存浏览器名称和版本号的字符串等同于 browser；

**鄙视题:** 如何判断正在使用的浏览器的名称和版本号?

- ↓ IE8-IE10: MSIE/版本号
- ↓ Firefox: Firefox/版本号
- ↓ OPR: OPR/版本号 Chrome/版本号 Safari/版本号
- ↓ Edge: Edge/版本号 Chrome/版本号 Safari/版本号
- ↓ Chrome: Chrome/版本号 Safari/版本号
- ↓ Safari: Safari/版本号

```html
<script>
  var ua = navigator.userAgent;
  var browser, version;
  //猜ua中有没有IE
  if (ua.indexOf("IE") != -1) {
    browser = "IE";
  }
  //如果没有IE，却有Trident，说明一定是IE 11
  else if (ua.indexOf("Trident") != -1) {
    browser = "IE";
    version = 11;
  }
  //再猜ua中有没有火狐
  else if (ua.indexOf("Firefox") != -1) {
    browser = "Firefox";
  }
  //再猜ua中有没有OPR
  else if (ua.indexOf("OPR") != -1) {
    browser = "OPR";
  }
  //再猜ua中有没有Edge
  else if (ua.indexOf("Edge") != -1) {
    browser = "Edge";
  }
  //再猜ua中有没有Chrome
  else if (ua.indexOf("Chrome") != -1) {
    browser = "Chrome";
  }
  //再猜ua中有没有Safari
  else if (ua.indexOf("Safari") != -1) {
    browser = "Safari";
  }

  if (version === undefined) {
    //1. 先在ua中查找浏览器名称出现的位置
    var i = ua.indexOf(browser);
    //2. i+浏览器名称的长度+1
    i += browser.length + 1;
    //3. 截取ua中i位置开始的后三位字符，转为浮点数
    version = parseFloat(ua.slice(i, i + 3));
  }
  document.write(`${navigator.userAgent}<hr>${browser}<hr>${version}`);
  console.log(navigator.userAgent);
  /*Mozilla/5.0 (Windows NT 10.0; WOW64)  
    AppleWebKit/537.36 (KHTML, like Gecko)  
    Chrome/75.0.3770.100 Safari/537.36*/
  console.log(browser); //Chrome
  console.log(version); //75
</script>
```
