# Ajax

## 同步Synchronous

在一个任务进行的过程中，不能开启其它任务  
同步访问：浏览器在向服务器发送请求时，浏览器只能等待服务器响应，不能做其他事  
同步访问的出现场合：  

- 地址栏输入url，是同步访问
- a标签跳转
- form提交

## 异步Asynchronous

在一个任务开启时，可以进行其它的任务  
异步访问：浏览器在向服务器发送请求时，用户可以在页面上做其它的操作  
使用异步的场合：

- 用户名重复的验证
- 聊天室
- 百度搜索建议
- 股票走势图

## 什么是ajax

Asynchronous  JavaScript  And  XML  
异步的=======>js      和===>xml  
本质：使用js提供的异步对象,异步的向服务器发送请求，并接收响应回来的数据  
异步对象: XMLHttpRequest(js提供)  

## 使用ajax

①创建异步对象 ②创建请求 ③发送请求 ④接收响应数据

1. 创建异步对象  
`var xhr=new XMLHttpRequest();`  
这种创建方式，不兼容IE8以下的版本  
下面是兼容ie8以下版本的创建方式  
```js
if(window.XMLHttpRequest){//如果有这个属性，说明是IE8以上的浏览器  
    var xhr=new XMLHttpRequest();  
    }else{//如果没有这个属性,说明是IE8以下的浏览器  
    var xhr=new ActiveXObject('Microsoft.XMLHttp');
    }  
```
2. 创建请求，打开连接  
`xhr.open(method,url,isAsyn);`  
method：string类型，请求的方法  
url:string类型,请求的url  
isAsyn:bool类型，是不是要采用异步的方式提交请求  
1. 发送请求
`xhr.send(formdata);`  
注意：只有post请求，才有请求主体formdata  
get方法不需要请求主体。  
所以使用get请求的时候，有两种发送请求的写法  
`xhr.send()`,`xhr.send(null)`  
1. 接收响应  
- xhr.readyState属性  
用于表示xhr对象的 请求状态  
一共有5个状态  
0：请求尚未初始化  
1：已经打开连接，请求正在发送中  
2：接收响应头  
3：接收响应主体  
4：接收响应数据成功  
- xhr.onreadystatechange  
监听xhr.readyState值的改变，每改变一次，方法会调用一次，一共会调用4次。  
注意：只有当xhr.readyState=4的时候，是我们要接收响应正确时刻  
- xhr.status响应状态码  
只有响应状态码为200的，我们才接收响应  
- xhr.responseText,响应数据放在了xhr.responseText属性中  
```js
xhr.onreadystatechange=function(){
    if(xhr.readyState==4&&xhr.status==200){
    var result=xhr.responseText;
     console.log(result);
   }
}  
```

## ajax带参数的get请求

略

## ajax的post请求

使用post方法发送请求  
1. xhr.open，需要改成post方法  
1. xhr.open中的url，不需要？和参数了  
1. 添加创建请求主体的代码，把数据放到请求主体中  
1. 修改请求消息头，可以发送特殊符号  
1. xhr.send(请求主体)  
```js
//url不要?和后面参数
var url="http://127.0.0.1:8080/ajax/login_post";
xhr.open("post",url,true);
//创建请求主体
var formdata="uname="+u_name+"&upwd="+u_pwd;
//由于ajax默认传输是text/plain
//无法传递特殊符号，我们需要更改消息头
//让ajax请求可以传递特殊符号
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
xhr.send(formdata);  
```

## Json的解析

- js对象的数据格式  
`var obj={name:"abc",age:18}`  
语法：var 对象名称={属性1：值1，属性2：值2.....}  
注意：**js对象中，属性名没有双/单引号**  
- JSON数据格式  
  json是一个string字符串，亲切的称之为json串  
  JavaScript object Notation  
    js======对象 == 表示法  
  以js对象的格式表现出来的字符串  
- json字符串的格式  
  - 用一对{}表示一个对象
  - json中对象的属性名，必须使用""引起来(使用单引号也是正确的，但是不推荐)
  - 属性的值如果是字符串，也要带双引号
  - json的表现是一个字符串，所有最外层加引号(推荐使用单引号)
  - 请求访问服务器，调用数据库代码，得到的结果，默认是一个json串
- json解析:把json字符串转换成js对象数组  
`var arr=JSON.parse(result);`

## XML的解析

### 什么是XML  

eXtensible Markup Language  
可拓展 === 标记 ==   语言  
是html的一个变种，专门负责承载数据用的  
xml中标签，关键字/属性都需要自己定义  
语法  

1. 第一行写版本声明  
`<?xml  version="1.0" encoding="utf-8"?>`
1. xml的标记只有双标记，必须成对出现
1. xml的标签严格区分大小写，开始标签和结束标记必须一致
1. xml标记，允许嵌套，但是要注意嵌套顺序
1. 每个xml文档，有且只有一个根元素

```xml
<?xml  version="1.0" encoding="utf-8"?>
<studentlist>
    <student>
        <name>tom</name>
        <age>18</age>
        <gender>男</gender>
    </student>
    <student>
        <name>lucy</name>
        <age>21</age>
        <gender>女</gender>
    </student>
    <student>
        <name>lilei</name>
        <age>21</age>
        <gender>男</gender>
    </student>
    <student>
        <name>hanmeimei</name>
        <age>20</age>
        <gender>女</gender>
    </student>
</studentlist>
```

### xml解析

使用dom解析  
result.getElementsByTagName("student")  

- 不能使用xhr.responseText获取xml。这样获取的xml不能解析。  
要使用var result=xhr.responseXML;

```html
<script>
    function getxml(){
        //1.创建xhr异步对象
        var xhr=new XMLHttpRequest();
        //4.获取相应数据
        xhr.onreadystatechange=function(){
            if(xhr.readyState==4&&xhr.status==200){
                //1.使用responseXML才能解析
                var result=xhr.responseXML;
                console.log(result);
                //2.先获取根元素studentlist
                var studentlist=result.getElementsByTagName("studentlist")[0];
                //3.获取student标签16:15~16：30休息
                var student=studentlist.getElementsByTagName("student")[1];
                //4.获取name标签
                var uname=student.getElementsByTagName("name")[0];
                console.log(uname.innerHTML);
            }
        }
        //2.打开连接，创建请求
        xhr.open("get","http://127.0.0.1:8080/students.xml",true);
        //3.发送请求
        xhr.send();
    }
</script>
```