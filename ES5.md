# ES5

<!-- TOC depthFrom:2 orderedList:false -->

- [严格模式](#严格模式)
- [保护对象](#保护对象)
- [call-apply-bind](#call-apply-bind)
- [数组API](#数组api)

<!-- /TOC -->

>ECMAScript: javascript语言的国际标准  
仅定义了js语言的基本语法  
没有定义如何操作网页内容  
问题: JavaScript的语言诞生极其草率，有很多广受诟病的缺陷。  
ES5: 是ECMAScript制定第五版js语言的标准

## 严格模式

WHAT: 比普通js运行机制要求更严格的模式  
WHY: 为了改善js中很多广受诟病的缺陷  
WHEN: 所有js程序都要运行在严格模式下  
HOW: 只要在当前代码的顶部添加: "use strict"  

新的要求:  

1. 禁止给未声明的变量赋值:  
  旧js中: 给未声明的变量赋值，不会报错，而是在全局创建该变量——造成全局污染。  
  严格模式: 给未声明的变量赋值，报错！xxx is not defined!  
2. 静默失败升级为错误:  
 什么是静默失败? 执行不成功还不报错！  
 ES5严格模式中: 将所有静默失败都变为报错！  
3. 普通函数调用或匿名函数自调中的this，不再指向window，而是undefined。  
4. 禁止使用arguments.callee:  
     arguments.callee( )  在当前函数执行内部，再次调用当前函数自己！——专门用于做递归调用。  
     递归2个问题:  
     1. 紧耦合: 在函数内写死函数名，将来函数名变化，函数内部被迫跟着修改。  
       解决: arguments.callee-> 自动获得当前函数本身，而不用管函数名  
     2. 致命问题: 重复计算量太大！递归效率极低！  
       严格模式禁用arguments.callee，就意味着，禁用了递归算法！  
       解决: 绝大多数递归，都可用循环代替！  

## 保护对象

WHAT: 防止对对象的成员或结构做一些无意义的篡改。  
WHY: js中的对象，毫无自保能力  
HOW: 2大块内容:  

1. __保护单个属性的值__(2种):  
    1. 保护普通数据属性的值:  
       数据属性: 值直接保存在属性的属性  
       HOW: 其实ES5中，对象的每个数据属性，都变成了一个缩微的小对象，每个缩微的小属性对象中都包含1个属性值和3个开关属性:  
        - value: 实际存储属性值,  
        - writable: 控制是否可修改当前属性值,  
        - enumerable: 控制是否可被for in 遍历到  
              问题: 虽然可防住for in，但用对象.的方式依然可强行访问。  
        - configurable: 控制是否可删除该属性  
                   控制是否可修改前两个开关  
                   一旦改为false，不可逆  
                   所以当设置其他两个开关时，都带上configurable:false，作为双保险。  
        如果修改属性的开关:  
            1. 只修改一个属性的开关:  
                (重新)定义 obj的指定属性  
              Object.defineProperty(obj, "属性名", {  
                 开关: true/false,  
                 开关:true/false,  
              })  
            1. 同时修改多个属性的开关:  
           Object.defineProperties(obj,{  
             属性名: {  
               开关: true/false,  
                ... : ... ,  
             },  
             属性名: {  
               开关: true/false,  
                ... : ... ,  
             },  
           })  
      问题: 使用开关保护属性，只能提供基本的单调的保护。无法根据自定义规则保护属性。  
       比如: 年龄必须介于18~65之间  
    1. 用自定义规则保护属性值:  
       访问器属性:  
       什么是: 保镖，不实际存储属性值，专门提供对另一个数据属性的自定义保护。  
       何时: 只要使用灵活的自定义规则保护属性时，都要请保镖。  
       如何: 3步:  
       <ol>
        <li> 前提: 先定义一个半隐藏的受保护的数据属性，实际存储属性值。<br>  
        且数据属性名不要用正式属性名，最好_开头，以示区分。 <br>  
          Object.defineProperty(eric,"_age",{ <br>  
            value: 26,<br>  
            writable:true, //可以改<br>  
            enumerable:false, //半隐藏<br>  
            configurable:false //双保险<br>  
          })</li><br>  
        <li> 请保镖: 一请，就是一对儿<br>
          一个保镖叫get函数, 专门负责从受保护的数据属性中取值  <br>
          另一个保镖叫set函数，专门负责将要修改的值，保存回数据属性中。  <br>
          但是，set函数通常都会对传入的新值进行验证！只有验证通过，才保存回去。如果验证不通过，不保存，且报错！  <br>
         <pre>Object.defineProperty(eric,"age",{  
            get:function( ){ return this._age },  
            set:function(value){  
              //value会自动接住要赋的新值  
              if(value>=18&&value<=65){  
                this._age=value;  
              }else{  
                throw Error("年龄必须介于18~65之间")  
              }  
            }  
          })  </pre> </li>
        <li> 保镖何时发挥作用:  <br>
         当试图用保镖获取属性值时，自动调用get()<br>
         比如: console.log(eric.age)<br>
                自动调用age:{ get:function(){ ... }  }<br>
         当试图用保镖给属性赋值时，自动调用set()，且自动将要赋的新值，传给value形参，先验证<br>
         比如: eric.age=27 会自动调用age:{ set:function(value){ ... } }<br>
        总结: 单从使用上来看:  <br>
        访问器属性的用法和普通属性完全一样！<br>
        只不过，运行机制，不同。<br>
       </li></ol>
1. __保护对象结构:__  
保护结构: 3个级别:  
    - 防扩展: 禁止给对象添加新属性  
     Object.preventExtensions(obj)  
      阻止对obj对象扩展任何新属性  
      问题: 只能防止添加新属性  
           不能防止删除现有属性  
    - 密封: 在兼具防扩展同时，禁止删除现有属性  
     Object.seal(obj)  
        1. 自动调用preventExtensions()阻止扩展  
        2. 自动将所有属性的configurable开关都改为false!  
    将来一个对象的结构，保护到seal密封程度就够了。  
    - 冻结: 在兼具密封的基础上，又进一步禁止修改所有属性值。  
     Object.freeze(obj)  
        1. 自动调用seal( )密封了obj  
        2. 自动将所有属性的writable：false  

<!-- Object.create():
  什么是: 基于一个现有的父对象，创建子对象，自动设置继承关系
  何时: 没有构造函数，不能new时，也想创建子对象
  如何: 
   var child=Object.create(father,{
     属性1:{ value + 三个开关},
       ... : ...
   })
    1. 创建一个新的空对象child
    2. 自动设置child继承father
    3. 为child添加自有属性 -->

## call-apply-bind

>call( ) &nbsp; &nbsp; apply( )&nbsp; &nbsp; bind( )

相同: 都是用来替换函数中不正确的this  
何时: 只要函数中的this不是想要的，都可随意替换  
如何: 2种  

1. 在调用函数时，临时换一次:  
函数.call(替换this的对象, 实参值列表...)  
比如: calc.call(lilei, 10000,1000,2000)  
   1. call是调用的意思，先调用calc函数
   2. call将第一个参数对象替换calc中的this
   3. call会将后续实参值列表注射入calc中传给形参  
问题: 如果不确定要注入的实参值个数，可用数组向函数中注入实参值列表。传入要调用的函数中。
2. 创建一个和原函数一模一样的函数副本，并永久绑定this为指定的对象:  
 var newFun=old_fun.bind(替换this的对象)  
 原理:  
   1. bind会创建一个和原函数一幕一样的新函数副本——只创建，并未调用  
   2. 将新函数中的this，永久绑定为指定的对象  
 结果: 从此，调用新函数时，不用再每次都临时替换this  

总结:  
只要函数调用时，其中的this不是想要的，就可用call/apply/bind替换  

1. 如果只在本次调用时，临时替换一次，就用call( )  
   如果给定的实参值是放在数组中的，则用apply( )先打散，再调用函数，并传入。
2. 如果希望永久绑定this时，就用bind( );

## 数组API

1. 查找元素:  
   var i=arr.indexOf("元素值",starti)  
   在arr中，从starti位置开始，找下一个匹配的元素的位置i  
   如果找到，返回元素的位置  
   如果找不到，返回-1  
2. 判断: 判断数组中的元素是否符合要求
   1. 判断数组中的元素是否都符合要求:  
     var bool=arr.every(function(elem, i, arr){  
       //回调函数: 自动在每个元素上执行一次  
       //每次调用时，都会拿到三个值:  
       //  elem 自动获得当前正在遍历的元素值  
       //  i  自动获得当前正在遍历的元素位置  
       //  arr  自动获得当前正在遍历的整个数组对象  
       return 判断条件  
     })  
     原理: 如果将回调函数去每个元素上都调用一次，都返回true，整个every才返回true  
           如果调用过程中，只要有一个元素返回false，则整个every返回false  
   2. 判断数组中是否包含符合要求的元素:  
     var bool=arr.some(function(elem,i,arr){  
       return 判断条件  
     })  
     原理: 只要有一个元素判断返回true，整个some()就返回true。  
          除非所有元素判断后都返回false，整个some()才返回false  
3. 遍历: 对数组中每个元素执行相同的操作(2种)。  
   <ol><li> 对原数组中的每个元素执行相同的操作<br>
     arr.forEach(  <br>
      //for(var i=0;i&lt;arr.length;i++)  <br>
      function(elem,i,arr){  <br>
   //不需要返回值  <br>
      }  <br>
     )  </li><br>
   <li> 取出原数组中每个元素，执行相同操作后，放入新数组中返回<br>
    var newArr=arr.map(<br>
      //先创建一个新的空数组<br>
      //var newArr=[]<br>
      //再对每个元素调用回调函数<br>
      //for(var i=0;i&lt;arr.length;i++)<br>
      function(elem,i,arr){<br>
        return 处理后的新值<br>
      }<br>
      //每次调用回调函数后，都会将本次调用的结果放入新数组中对应位置<br>
      //->newArr[i]<br>
      //返回新数组<br>
      //return newArr;
    )</li></ol>

4. 过滤和汇总:  
    1. 过滤: 复制出数组中符合条件的元素，组成新数组  
    var newArr=arr.filter(  
    //var newArr=[];  
    //for(var i=0;i&lt;arr.length;i++)  
    function(elem,i,arr){  
    //自动在每个元素上执行一次  
     return 判断条件  
    }//只有返回true的元素，才被复制到新数组中保存  
    //return newArr;  
    )  
    2. 汇总: 对数组内的元素进行求和汇总  
    var sum=arr.reduce(  
    //var prev=0;  
    //for(var i=0;i&lt;arr.length;i++){  
    function(prev,elem,i,arr){  
    //prev接住的是，截止到目前的临时汇总值  
    return prev+elem; //将当前元素值累加到临时汇总值  
    }//将本次累加的值再放回prev中  
    //return prev  
    )  
