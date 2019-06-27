# jQuery

## 什么是 jQuery

jQuery 是 **第三方** 开发的执行 DOM 操作的 **极简化** 的 **函数库**。

- 第三方  
  由除了浏览器原生的以及咱们自己编写的之外，其组织或个人开发的框架/库——要下载。  
  执行 DOM 操作: jQuery 还是在执行 DOM 的增删改查和事件绑操作。——学 jQuery，还是在学 DOM。
- 极简化: jQuery 是对 DOM 操作的对象和函数进行的简化。
- 函数库: jQuery 中使用函数解决一切问题。jQuery 中一切都函数！。

何时使用 jQuery:  
几乎所有大项目或框架的底层，都是用 jQuery 开发的。——仅适合于 PC 端项目

为什么使用:

1. 简单
2. 兼容性: 凡是 jQuery 让用的，都没有兼容性问题:  
   比如: IE8 不支持 nth-child(i)  
   但是 jQuery 可随便使用 nth-child(i)  
   因为 jQuery 内部其实调用的还是原生的 DOM 函数，且一旦发现不兼容，立刻用 js 程序模拟。  

何时使用 jQuery:  
几乎所有大项目或框架的底层，都是用 jQuery 开发的。——仅适合于 PC 端项目

## 如何使用 jQuery

下载: www.jquery.com  
版本:

- 1.x 兼容旧的浏览器  
  jquery-1.11.3.js //未压缩  
  优点: 可读性好，适合学习和开发之用  
  缺点: 体积大，不便于下载和传输  
  jquery-1.11.3.min.js //压缩  
  优点: 体积小，便于快速下载和传输  
  缺点: 毫无可读型。
- 2.x 不再兼容旧浏览器
- 3.x 不再兼容旧浏览器，且添加了新功能

引入:  
先引入 jquery-1.11.3.js，再编写自定义 js 代码。  
因为 DOM 操作包含大量查找操作，所以 **js 代码必须在 body 结尾引入，才能保证查找到任何想要的元素**。  
原理:  
引入 jquery-1.11.3.js 时，其实是在内存中创建了一个新类型叫 jQuery，  
包括

1. 构造函数:  
   负责创建 jQuery 类型的子对象
2. 原型对象:  
    负责保存所有 jQuery 的子对象共用的简化版函数，  
    比如:  
    .click( ) .html( )都保存在 jQuery.原型对象中  
    因为 DOM 元素不是 jQuery 家的孩子，所以，DOM 元素不能直接使用 jQuery 家简化版函数。  
    只要想使用 jQuery 操作 DOM，都要先创建 jQuery 类型的子对象。同时，使用选择器查找到 DOM 树上要操作的元素。将元素保存到 jQuery 子对象中。
   var $btn=new jQuery("#btn1")
    强调: 为了将jQuery家孩子和DOM家孩子区分，jQuery家孩子的变量都要以$开头——不是必须。
   jQuery 家的孩子，就可以调用原型对象中的简化版函数操作自己内部封装的找到的 DOM 元素了。
   对 jQuery 家孩子调用简化版函数，等效于自动对内部封装的 DOM 元素调用原生的函数。
   比如: $btn.click() =>  
         会被自动转换为 => btn.addEventListener("click",...)
  强调: 原DOM中事件处理函数中的this，获得是DOM家的孩子。不能直接使用jQuery家的函数。所以:  
   必须先var $btn=\$(this)，将 this 放入一个 jQuery 家的孩子中，才能使用 jQuery 家简化版函数。
   强调: jQuery 家的函数和对象，与 DOM 一定不能混用！
   决定用 jQuery，就要通篇都用 jQuery。

jQuery 函数的三个特点:

1. 几乎所有的函数都自带遍历:  
   因为 jQuery 子对象其实是一个可保存多个 DOM 元素的 **类数组对象**。  
   所以，对整个 jQuery 子对象调用一次简化版函数，相当于对内部的每个 DOM 元素都调用一次。  
   不用自己写遍历！
2. 多数函数都是一个函数两用:  
   调用时如果没给新值，就获取原值。  
   调用时如果给了新值，就变为修改值。  
    比如：  
    $btn.html() : 获取btn的内容  
   $btn.html("xxx") : 修改 btn 的内容  
3. 几乎每个函数都返回正在使用的 jQuery 对象，可继续使用。  
   强调: 因为\$是即创建新对象，又查找 DOM 树，所以，应该尽量少用！  
   解决: 链式操作！  
   注意: 做事儿的步骤，上一步的返回值，刚好是下一步的主语。  

## 查找元素

jQuery 只有两种查找:

### 按选择器查找

如何:  
 var $元素们=$("选择器")  
 $( )里，可以写所有css选择器，都支持！  
      另外，jQuery也扩展了少量新的选择器——只能在jQuery的$( )中使用

新选择包括:

1. 基本过滤/位置过滤:  
   什么是:  
   先将符合条件的元素，都取出来，放在一个集合中统一编号,且下标从 0 开始。  
   包括:  
:first  
:last  
:eq(i)  
:gt(i)  
:lt(i)  
:even  
:odd  
   vs 子元素过滤:  
   按照元素在其父元素内的相对编号选取元素，下标从 1 开始。  
   :first-child  
   :last-child  
   :nth-child(i)  
   :nth-child(2n)  
2. 内容过滤:
   1. 用元素内容中的文本作为筛选条件  
      :contains(文本)
   2. 用元素内部的子元素拥有的特征来鉴别父元素  
      :has("选择器")
3. 可见性过滤: 根据元素是显示还是隐藏，来选取元素
   :visible 选择未隐藏的元素  
   :hidden 选择隐藏的元素  
   强调: hidden 只能找到 display:none，和 type="hidden"两种隐藏的元素
4. 表单元素过滤:  
   :input 选择所有表单元素: input textarea select button  
   其实 jQuery 为每种 type 都提供了专门的选择器:  
   :text 选择普通文本框 <input type="text"  
   :password 选择密码框 <input type="password"  
   :radio 选择单选按钮 <input type="radio"  
   :checkbox 选择复选框 <input type="checkbox"  
   :button 选择按钮 <input type="button"  
   ...
5. 状态过滤:  
   :enabled 选择启用的元素  
   :disabled 选择被禁用的元素  
   :checked 选择被选中的 checkbox 或 radio 元素  
   :selected 选择 select 中被选中的 option  

### 按节点间关系查找

- 父子关系
  .parent( ) <== .parentNode  
  .children( ) 获得直接子元素  
  .children("选择器") 只选择符合选择器要求的直接子元素  
  何时: 如果只在直接子元素中查找  
  .find("选择器") 在所有后代元素中查找符合条件的元素  
  何时: 如果希望在所有后代中查找时  
  .children(":first-child") <== .firstElementChild  
  .children(":last-child") <== .lastElementChild
- 兄弟关系  
  .prev( ) <== .previousElementSibling  
  .prevAll(["选择器"]) 在当前元素之前的所有兄弟中查找符合条件的。  
  .next( ) <== .nextElementSibling  
  .nextAll(["选择器"]) 在当前元素之后的所有兄弟中查找符合条件的  
  .siblings(["选择器"]) 选择除自己之外的所有兄弟。不分前后。

## 1. 修改: 同 DOM

### 内容

1. 原始 HTML 片段:  
   .html(["新内容"]) <== .innerHTML
2. 纯文本内容:  
   .text(["新内容"]) <== .textContent
3. 表单元素的值:  
   .val(["新值"]) <== .value

### 属性

1. HTML 标准属性: 2 种:  
   核心 DOM 的函数：a.getAttribute()/setAttribute()
   HTML DOM ： a.href
1. 状态属性:  
   只能用.disabled .checked 修改
1. 自定义扩展属性:  
   a.setAttribute()/getAttribute()

**网页上** 可直接看到的属性: Attribute  
 HTML 标准属性和自定义扩展属性  
 上边的都能用.getAttribute()/. setAttribute()

jquery，都改为.attr("属性名"[, "属性值"]) 一个函数两用

++++++++++++++++++++++++++++++++++++++++++++++++++++

**内存中** 必须用 console.log()才能看到的属性: Property  
HTML 标准属性和状态属性  
下边的都能用.直接访问——jq 中没有属性，只有函数  
jquery 中都改为.prop("属性名"[, "属性值"])  
比如:  
获取 a 的 href 属性:  
$a.attr("href") / $a.prop("href")  
修改 a 的 data-target 属性值为"content1"  
$a.attr("data-target","content1")  
修改a的disabled为true  
$a.prop("disabled", true )  
简写:  
同时修改一个元素的多个属性:  
\$元素.attr 或 prop({  
属性名: "属性值",  
... : ...  
})

### 样式

获取或修改一个 css 属性的值:  
$元素.css("css 属性名"[, "属性值"])  
如果同时修改多个 css 属性:  
$元素.css({  
css 属性名: "属性值",  
... : ...  
})  
如果批量修改 css 属性，都首选 class 来操作:  
添加 class: $元素.addClass("class 名")  
$元素.removeClass("class 名")  
$元素.hasClass("class 名")==> $元素. is (".class 名")  
在有或者没有一个 class 之间来回切换:  
$元素.toggleClass("class 名")  
比如: $元素.toggleClass("down");  
在内部自动执行了:  
if(!$btn.hasClass("down")){  
$btn.addClass("down")  
}else{//否则，就抬起  
\$btn.removeClass("down")  
}  
强调:  
.toggleClass( )不能代替.addClass( )或.removeClass( )  
如果只是想添加 class，没想去掉 class，首选 addClass( )  
除非真的想在有和没有这个 class 之间来回切换时，才能选择 toggleClass( )  
**强调: 所有修改函数都是一个函数两用！**

## 添加/删除/替换/克隆

### 添加: 2 步

1. 用 html 片段创建 DOM 元素  
   var $新元素=$(`html片段`)
2. 将 DOM 元素添加到 DOM 树上  
    将新元素添加到 DOM 树上
   - 末尾追加:  
      $父元素.append ($新元素) return $父元素=> .appendChild();  
      简写: $父元素.append (`html片段`);  
      $新元素.appendTo($父元素) return $新元素;  
      简写: $新元素.appendTo("父元素选择器");  
      比如: 将新元素添加到父元素后，要修改父元素的宽度;  
      $父元素.append ($新元素).css("width",500) - 将新元素添加到父元素后，要为新元素绑定事件  
      $新元素.appendTo($父元素).click(function(){ ... })
   - 开头插入:  
     $父元素.prepend($新元素)  
     $ 新元素.prependTo($父元素)
   - 在现有元素前插入:  
      $现有元素.before($新元素) return $现有元素==> .insertBefore()  
         $新元素.insertBefore($现有元素) return $新元素
   - 在现有元素后插入:  
      $现有元素.after($新元素) return $现有元素=> .insertBefore()  
         $新元素.insertAfter($现有元素) return $新元素
   - 替换元素:  
     $现有元素.replaceWith($新元素,) return $现有元素=> .replaceChild()  
        $新元素.replaceAll($现有元素) return $新元素
3. 删除: \$元素.remove();
4. 克隆元素: \$元素.clone();

## 事件绑定

DOM 中: .addEventListener("事件名", 处理函数)
.removeEventListener("事件名", 处理函数)
坑: 如果一个处理函数可能被移除，则绑定时就要用有名称的函数。移除时，也要用函数名来移除。
jQ 中: .on("事件名", 处理函数)
对 21 种常见的事件，提供了更简化的写法:
.事件名(处理函数)
比如: .click(function(){ ... }) ...
.off("事件名", 处理函数)
事件委托/事件代理:
$(父元素).on("事件名","选择器",function(e){
   //on执行了: this=e.target;
   var $tar=$(this); //$(e.target);
if(\$tar.is("选择器")){//on 把选择器拿走自动判断去了
//结果，凡是进入 function 中的，一定都是符合要求的
直接写正常的事件处理逻辑
}
})
两个福利: 1. on 拿走了选择器，自动判断，咱们不用再写 if 2. this->e.target，不用写 e 和 e.target

总结: \$有 4 种用途:

1. \$("选择器") 创建 jQuery 对象，并查找元素，封装进 jQuery 对象中
2. $(DOM元素) 直接将获得的DOM元素，包装为一个jQuery对象，可调用jQuery家的简化版函数
  比如： $(this) $(e.target)   $(txt)
3. \$(`html片段`) 用 html 判断创建新的元素

4. 事件:
   页面加载后，自动执行:
   问题 1: 如何保证无论 js 代码写在网页的开头还是结尾，都能正常执行呢？
   解决 1: 将所有的事件绑定代码都写在 window.onload=function(){ 中 }
   比如://当窗口的内容都加载完之后
   window.onload=function(){
   //才查找按钮绑定事件
   $("#btn1").click(function(){
        alert("疼！");
        })
        }
  问题2: window.onload=function(){}是用赋值方式绑定事件。整个窗口只能绑定一个处理函数。如果多个js文件中都包含window.onload=function(){}，结果只有最后一个会覆盖之前所有。如何让多个js文件中的window.onload=function(){}并存？
  解决: $(window).on("load",function(){
   //.addEventListener
   //可进一步简写为:
   $(window).load(function()
         
       })
  问题3: window.onload必须等待所有网页内容（HTML, JS, CSS, 图片）都加载完才能触发，才能绑定事件。用户有可能等不及要使用元素的功能！
    如何让用户不必等待css和图片，也能提前用上网页功能？
  解决: jQuery: 
  //当 DOM树 准备就绪 就提前触发
   $(document).ready(function(){
   $("#btn2").click(function(){
    alert("疼！");
   })
   })
  结论: 今后绝大多数页面初始化或事件绑定操作，都应该放在DOM树加载完就提前触发。
  简写: 
   $(function(){
   $("#btn2").click(function(){
    alert("疼！");
   })
   })
  总结: 今后所有jq代码，都应该放在$(function(){ ... })
   今后见到$(function(){ ... })就是"DOM树加载后就提前执行"的意思
   从此$(function(){ ... })代替了匿名函数自调成为所有程序的外层容器代码。

鼠标事件:
mouseover 鼠标进入 mouseout 鼠标移出
问题: mouseover 和 mouseout 默认是冒泡的。
也就是说反复进出子元素同样会反复触发父元素上的事件
且不能用 e.stopPropagation()解决，因为事件绑在最外层父元素上。不可能阻止所有子元素上来的冒泡。也不可能给每个子元素都绑定事件阻止冒泡。
解决: 就希望进出子元素，不再反复触发父元素上的事件
jQuery 中都是用.mouseenter()和.mouseleave() 代替 mouseover 和 mouseout
简写: 如果同时绑定鼠标进入和鼠标移出事件时:
jQuery 中可只绑定一个: .hover()
绑定一个.hover()，等效于同时绑定了 mouseenter()和 mouseleave()
但是 hover 中需要 2 个函数。一个给 mouseenter，另一个给 mouseleave。
$("#target")
  .hover(//=mouseenter+mouseleave
    function(){//给mouseenter
      $(this).addClass("hover")
},
function(){//给 mouseleave
$(this).removeClass("hover")
    }
  )
  极其特殊的简写: 如果两个处理函数刚好可以改为一致的，则只需要写一个处理函数即可。一个函数即给mouseenter，又给mouselieave
    比如: $("#target")
.hover(//=mouseenter+mouseleave
function(){//即给 mouseenter 又给 mouseleave
\$(this).toggleClass("hover")
}
)

模拟触发: 即使没有点击按钮，也可执行按钮上的事件处理函数
如何: \$(处理函数所在的元素).trigger("事件名")
触发
//可简写为: .事件名()

## 动画:

1. 简单动画: 固定的三种动画效果:
   1. 显示隐藏: .show() .hide() .toggle()
      默认: 代替 display:block 和 display:none 实现瞬间显示隐藏
      所以，如果只是想显示隐藏，不带动画效果，show(), hide(), toggle()还是很好用的！
      如果给函数添加 ms 数参数，就变成带动画的版本
   2. 上滑下滑: .slideUp() .slideDown() .slideToggle()
   3. 淡入淡出: .fadeIn() .fadeOut() .fadeToggle()
      简单动画函数致命的两个问题:
   4. 在 jQuery 源代码中写死的动画效果，无法维护。
      vs css 动画: 极其便于维护
   5. 都是用 js 定时器模拟的: 效率低！
      vs css 动画: 由专门的绘图引擎解析，效率高！
2. 万能动画: 可对任意 css 属性应用过渡的动画函数
   \$元素.animate({
   css 属性: 目标值,
   ... : ...
   },动画持续时间)
   执行效果: animate 自动获得当前元素状态和 css 属性值，再与目标值比对，执行过渡动画效果。
   问题: 只支持单个数值的 css 属性
   不支持: 颜色过渡， CSS3 变换


    排队和并发:
     排队: 多个css属性先后依次变化:
      如何: 对同一个元素，先后调用多次animate，就实现排队执行。
      原理:
       其实，每个元素都有一个动画队列: [       ]
       animate其实不是播放动画的意思
       而是将现有动画定义假如到元素的动画队列中
       动画何时执行取决于队列中前边有没有其他未执行完的动画。只有之前的动画都执行完，当前动画才自动开始
     并发: 多个css属性同时变化
      如何: 放在一个animate中的多个css属性默认并发变化

    动画结束后自动执行:
     其实每个动画函数都有最后一个形参，是一个回调函数。这个回调函数会在动画播放完成后自动被调用！

    停止动画: .stop()
      坑: 只能停止队列中当前正在播放的一个动画。
        队列中后续动画依然继续执行。
      解决: .stop(true) 清空队列
    选择器: :animated  专门用于判断或选取正在播放动画的元素

## 类数组对象操作:

问题: jQuery 返回的都是类数组对象，经常需要查找/遍历。但是在原生 js 中，类数组对象很受歧视。因为不是纯正的数组类型，所以数组家的函数，类数组对象都不能用。
解决: jQuery 模仿原生 js 中的 indexOf 和 forEach，重新定义了两个 index()和 each()函数，专门给类数组对象用。
包括:

1.  遍历 jQuery 对象中封装的每个 DOM 元素:
    $(...).each()  仿原生js中的arr.forEach()
     何时: 只要遍历jQuery结果中的每个DOM元素时
     如何:$(...).each(function(i, elem){
    //i 正在遍历的当前位置
    //elem 正在遍历的 DOM 元素
    //想用 elem 调简化版函数，必须\$(elem)一下
    })
2.  查找: 在 jQuery 对象中查找一个 DOM 元素出现的位置
    var i=$(全部元素).index(要找的元素)
     比如:  在所有li中找一个li的位置
      var i=$("ul>li").index($li)
     简写: 如果在一个父元素内，找某个子元素的位置，可简写为: $子元素.index() ——默认就只在当前父元素内找

## 添加自定义函数:

何时: jQuery 提供的函数不够用时
如何: 其实就是在 jQuery 的原型对象中添加一个新函数。所有 jQuery 类型的子对象都可共用！

总结: \$的原理: 共有四种用法:

1.  \$("选择器") 创建 jQuery 对象，并查找 DOM 元素
2.  \$(DOM 元素) 将已经获得的 DOM 元素包装为 jQuery 对象
3.  \$("html 片段") 创建 jQuery 对象，同时创建新的 DOM 元素
4.  \$(function(){ ... }) 绑定事件，在 DOM 内容加载后就自动触发

鄙视题: 你觉得我们公司的官网有哪些可以优化的地方:
F12->network->刷新页面
看请求次数: >50 次，算多的
可以说，减少请求次数: 1. 用 css 精灵图，减少图片的张数 2. 尽量减少 ajax 请求的次数，尽量一次获得全部元素
看个别进度条比较长的文件
可以说，降低图片质量，减小图片体积
压缩/合并 js 和 css 代码，减少代码的文件个数和体积

## \*\*\*封装自定义插件

1. 封装自定义插件:
   组件/插件: 拥有独立的 HTML，css，js 和数据的可重用的页面区域
   为什么: 重用!
   何时: 如果页面中一个功能区域可能被反复使用，都要将其封装为一个插件。
   如何: 2 种情况: 1. jQuery 官方插件: jQueryUI
   官网下载: jquery-ui.css
   images/
   jquery-ui.js
   在页面中引入:
   <link rel="stylesheet" href="css/jquery-ui.css"
   <!--先引入jquery，再引入jquery-ui-->
   <script src="js/jquery-1.11.3.js"
   <script src="js/jquery-ui.js"
   <script>自定义代码</script>
   html 中:
   按照插件的要求，定义 HTML 内容结构
   不需要加任何 class
   js: 查找插件的 HTML 父元素，对父元素调用一次插件函数即可自动添加样式和行为。
   \$("my-accordion").accordion();
   原理:
   侵入性: 插件函数根据自己的需要，自动为元素添加 class 和行为
   好处: 简单
   不好: 不可维护 2. 封装自定义插件:
   前提: 已经用 html，css 和 js 实现了插件的样式和功能。
   如何: 1. 将插件相关的 css，剪切到一个独立的 css 文件中保存。
   强调: 如何避免插件/组件间 class 冲突:
   一个组件内的选择器，都要以插件的父元素的 class 作为查找的开头/起点。 2. 定义独立的 js 文件：
   在 jquery 的原型对象中添加插件函数 1. 添加样式：侵入: 悄悄自动添加 2. 添加行为：
   使用自定义插件: 同 jQueryUI 的用法。

## ajax

jQuery 中已经封装好了现成的 ajax 函数，我们可直接调用
\$.ajax({
url:"url 路径",
type: "get/post",
data:"uname=dingding&upwd=123456",
//如果本次请求没有参数，可省略 data
dataType: "json",
//按照国际标准所有服务端接口，都应该返回 json 格式的字符串。
//但是也不排除例外
//如果返回的不是 json，就不要写 dataType:"json"，会出错。
//因为 dataType:"json"是自动执行 JSON.parse()的意思。如果服务端返回的字符串不是 json 格式，则 JSON.parse()会报错！
//success 函数是一个回调函数，会在请求成功结束后，自动调用。参数 result，会自动获得服务端返回的值。而且已经被 JSON.parse()，范围为 js 对象了。
success:function(result){
... ...
}
})
//ES 6 promise 中
.then(function(result){
//result 获得的就是服务端返回的数据
})
强调: success: 和 .then() 二选一即可！

## **\***跨域:

什么是: 一个域名下的网站，向另一个域名下的服务端发送请求。
比如:
网页 服务端
http://www.a.com -------> http://www.b.com
http://a.tedu.com --------> http://b.tedu.com
http://localhost:8080 --------> http://localhost:3000
http://www.12306.cn --------> https://www.12306.cn
(:80) (:443)
http://127.0.0.1:3000 --------> http://localhost:3000
IP 域名

http://tedu.cn/index.html--------> http://tedu.cn/index/login
相对路径 相对路径
不算跨域！
问题: 浏览器禁止 ajax 请求跨域获取数据
原理:

1.  浏览器其实是发出了请求的。
2.  请求也确实成功了，返回的结果，也拿回来了
3.  因为响应结果中带着响应头，记录着数据来源的 IP 地址。所以，当浏览器查验服务端返回的数据时，发现响应头中的 IP 不是当前网页的 IP，不让用！
    报错: Access to XMLHttpRequest at 'http://localhost:3000/' from origin 'http://127.0.0.1:5500' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
    CORS: Cross Origin Resources Sharing
    跨 源头 资源 共享 策略
    浏览器禁止与当前网页不同来源的数据被使用

解决: 2 种:

1. 简单: 单靠 服务端配置响应头
   在服务端程序中，在发送消息之前:
   手动修改响应头:
   node.js ：
   res.writeHead(200,{
   "Access-Control-Allow-Origin":"http://客户端网页地址栏中的地址"
   })
2. 公司: JSONP —— 同时修改客户端和服务端程序才能可支持。

前后端分离: 见视频。
