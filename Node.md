# nodejs概述

>nodejs基于谷歌V8引擎，运行在服务器端的语言，基于JS

## 对比JS和nodejs

- JS运行在客户端浏览器，存在多个浏览器，容易产生兼容性的问题；nodejs在服务器端只有一个环境，不存在兼容性。
- 两者都有内置(ES)对象、自定义对象、宿主对象(根据执行环境的不同划分)
- JS用于网页中的交互效果，nodejs用于服务器的操作，例如web服务器创建，数据库操作，文件操作等

   nodejs.org  英文官网  
   nodejs.cn  中文网

## nodejs的特点  

- 单线程逻辑处理
- 非阻塞的异步I/O处理
- 支持数万个并发连接

## nodejs的应用场景  

- 基于社交网络的大规模web应用  
- nodejs不适合CPU密集型的应用  
   递归、数据加密解密、数据挖掘和数据分析  

## nodejs的执行方式

- 脚本模式  
node  c:/xampp/.../1.js
- 交互模式  
     node  回车   进入交互模式  
     两次ctrl+c   或者   .exit    退出交互模式  

## 全局对象

>全局作用域下的变量就是全局对象下的属性,  
全局对象下的函数就是全局对象下的方法,  
可以使用全局对象来访问:`nodejs: global`;

- 在交互模式下，声明的变量和创建的函数都属于全局下的，可以使用global来访问；
- 在脚本模式下，声明的变量和创建的函数都不属于全局下的，一个文件默认会创建一个独立的作用域，叫做**文件（模块）作用域**，防止污染全局。  

在浏览器下(js: window)，**文件中声明的变量或者创建的函数都属于是全局作用域下的**，会污染全局。

**global下的全局对象**:  

- console对象——控制台  
  - global.console.log()  打印日志
  - global.console.info() 打印消息
  - global.console.warn()  打印自定义的警告
  - global.console.error()  打印自定义的错误
  - global.console.time('自定义字符串')  开始计时
  - global.console.timeEnd('自定义字符串')  结束计时  
    自定义字符串前后保持一致
- process对象——进程  
  - process.arch  查看当前CPU的架构
  - process.platform  查看当前的操作系统
  - process.env  查看当前系统的环境变量
  - process.version  查看当前nodejs的版本号
  - process.pid  查看当前的进程编号
  - process.kill()   结束某个编号的进程
- Buffer对象——缓冲区  
**一块用于临时存储数据的内存区域**，  
可以存储文件数据、网络上传输的资源(视频、在线直播...)  
  创建Buffer :  
  `var buf=Buffer.alloc(5, 'abcde')`  
     buffer数据 :  \<Buffer 61 62 63 64 65>  
  将buffer数据转为字符串:  
  `buf.toString()`  

![buffer.png](https://i.loli.net/2019/07/30/5d400272855d262454.png)

## 全局函数

- parseInt
- parseFloat
- encodeURI
- decodeURI
- isNaN
- isFinite
- eval
- 一次性定时器  
 开启  
 `var timer=setTimeout(回调函数, 间隔的时间);`  
 当间隔的时间到了，执行回调函数，单位是毫秒  
 清除  
 `clearTimeout(timer);`  
- 周期性定时器  
 开启  
 `var timer=setInterval(回调函数,间隔的时间);`  
 每隔一段时间，执行一次回调函数  
 清除  
 `clearInterval(timer)`  
- 立即执行定时器(只有服务器端有这个函数)  
开启  
`var timer=setImmediate(回调函数)`  
回调函数会放入到队列中  
当主线程程序执行完，才会执行队列中的内容  
清除  
`clearImmediate(timer)`  
- `process.nextTick(回调函数)` ==> 立即执行定时器  
在主程序的末尾执行

```JS
//立即执行定时器
var timer = setImmediate(function() {
  //回调函数会放入到队列中
  //当主线程执行完，才会执行队列的内容
  console.log("查询数据--1");
});
//clearImmediate(timer);
//在主程序执行完，立即执行
//连接数据库
console.log("连接数据库");
process.nextTick(function() {
  console.log("查询数据--2");
});

//===> 连接数据库
//===> 查询数据--2
//===> 查询数据--1
```

## 模块

>模块就是一个封装好的功能体
>>在nodejs下模块分为自定义模块、核心模块(官方提供)、第三方模块

### 自定义模块

   在nodejs下，任意一个js文件都是一块模块，文件中的代码默认被一个**构造函数**所包含  

```js
(function(exports,require,module,__filename,__dirname){
  //程序员编写的代码
})
```

- __filename  当前模块的完整路径和文件名称
- __dirname  当前模块的完整路径
- require( )  引入一个模块
- module  指代当前的模块对象
- module.exports  当前模块导出的对象(默认为空对象{})，包含供其它模块使用的属性和方法
- exports 构造函数的形参，和module.exports指向同一个地址，即等价于module.exports

### 模块分类

|          |                                           以路径开头                                            |                                                           不以路径开头                                                            |
| :------: | :---------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------: |
| 文件模块 |           `require('./circle.js')`常用于用户自定义的模块，如果后缀名是js，则可以省略            |                                            `require('url')`用于引入官方提供了核心模块                                             |
| 目录模块 | `require('./02_2')`在02_2目录下寻找package.json中寻找main属性对应的文件，找不到会去引入index.js | `require('04_2')`自动到当前目录下的node_modules中寻找目录模块04_2，如果找不到会到上一级目录下寻找，直到顶级目录。常用于第三方模块 |

## npm和包

>包(package): 是一个目录模块，里边包含多个文件，其中有一个文件命名为package.json，是包说明文件，含有包的信息
>>npm: 包管理工具，安装nodejs的时候会附带安装，用于管理包，包括下载，上传，升级...

 npm官网： www.npmjs.com  

- 切换目录  
   cd  完整路径  
     如果要进入其它的盘符  
     d:   回车  
   进入指定目录下，按住shift键，在空白区域单击鼠标右键->在此处打开powershell  
- 使用npm下载安装第三方包  
   npm install 包名称  
- 生成package.json  
   `npm init -y`  
   自动生成一个package.json文件，后期使用npm 安装的包都会记录到这个文件中。  
- `npm install`  自动安装package.json文件中记录的包

## querystring模块——查询字符串

>**属于核心模块，nodejs官方提供的，可以直接引入，不需要创建**

 <http://www.codeboy.com/detail.html?lid=5&name=dell>  
 浏览器向服务器发请求，传递数据的一种方式  

- `querystring.parse()`  将查询字符串格式化为对象  
- `querystring.stringify()`  将对象转换成查询字符串  

## url模块

- `url.parse()`  将url格式化为对象
  - protocol`  协议
  - hostname`  服务器域名/IP地址
  - port`  端口号
  - pathname`  文件在服务器上的路径
  - query`  查询字符串
- `url.format(obj)`  将对象转成url  
   **query属性对应的是对象**

```js
//引入url模块
const url=require('url');
//url

var str='http://www.codeboy.com:80/product/detail.html?lid=5&name=dell';
//将url格式化为对象
var obj=url.parse(str);
console.log(obj.query);


//将对象转换成url
var obj={
  protocol:'http',
  hostname:'172.163.0.224',
  port:8080,
  pathname:'/admin/login.html',
  //search:'?uname=root&upwd=123456'
  query:{
    uanme:'root',
    upwd:'123456'
  }
}
var str=url.format(obj);
console.log(str);
```

## fs模块——文件系统模块

>用于文件的操作，目录的创建、删除、读取；文件的创建、读取、写入、删除..

- 查看文件状态  
   `fs.stat(path,callback) / statSync(path)`  
- 创建目录  
   `fs.mkdir(path,callback) / mkdirSync(path)`  
- 移除目录  
   `fs.rmdir(path,callback) / rmdirSync(path)`  
- 读取目录  
   `fs.readdir(path,callback) / readdirSync(path)`  
     callback  
        err  可能产生的错误信息  
        files   读取的结果，格式为**数组**  
- 清空写入(不存在则创建)  
  `fs.writeFile(path, data, callback) / writeFileSync()`  
   path  要写入的文件的路径  
   data  要写入的数据  
   callback  回调函数  
  如果文件不存在会创建文件，  
  如果文件已经存在，会清空文件中的内容，然后写入  
- 追加写入(不存在则创建)  
  `fs.appendFile(path,data,callback)/appendFileSync()`  
  如果文件存在，在文件的末尾写入数据
- 读取文件  
  `fs.readFile(path, callback)/readFileSync()`  
    callback  
      err  可能产生的错误信息  
      data  读取的文件中的数据，**格式为buffer** ==> data.toString()  
- 删除文件  
   `fs.unlink(path, callback) / unlinkSync()`  
- 判断文件(目录)是否存在  
   `fs.existsSync(path)`  
    存在->true  
    不存在->false

## http协议

>是浏览器和web服务器之间的通信协议

- 通用头信息(General)  
  - Request URL: 请求的URL，对应浏览器地址栏的内容，要向服务器获取哪些内容  
  - Request Method: 请求的方法，GET/POST...，获取内容的方式  
  - Status Code: 响应的状态码,可以查看到响应的结果  
    - 1**: 正在请求，没有结束  
    - 2**: 成功的响应  
    - 3**: 响应的重定向，跳转到另一个URL;通常结合响应头信息中Location一起使用  
    - 4**: 客户端错误  
    - 5**: 服务器错误  
  - Remote Address: 请求的服务器的IP地址和端口号
- 响应头信息(ResponseHeaders)  
  - Connection: 连接的方式，keep-alive 持续连接
  - Content-Type:响应的文件类型
  - Content-Length: 响应的文件长度
  - Transfer-Encoding: 传输方式 chuncked 分段传输
  - Content-Encoding: 压缩模式  gzip
  - Location: 当响应重定向的时候，跳转的URL
- 请求头信息(RequestHeaders)  
  - Accept: 客户端接受的文件类型有哪些
  - Accept-Encoding: 客户端接受的压缩形式
  - User-Agent: 客户端发请求使用的浏览器
- 请求主体  
   可有可无，客户端向服务器端传递的数据

## http模块

>既可以模拟浏览器向web服务器发请求，也可以创建web服务器

- 模拟浏览器  
   http.get( url, callback )  
========>get  请求的方法  
========>callback  回调函数，用于获取服务器端的响应  
============>res  响应的对象  
===============>statusCode   响应的状态码  
===============>res.on('data', function(buf){   })  
      通过事件获取服务器端的响应，当有数据传输的时候自动触发；  
      通过回调函数来接收数据；buf就是传输的数据，格式为buffer。  

```js
//引入http模块
const http=require('http');

//模拟浏览器向web服务器发请求
//get: 请求的方法
//参数1: 请求的URL
//参数2: 回调函数,用于获取服务器端响应
http.get('http://www.codeboy.com',function(res){
  //res: 响应的内容，格式为对象
  //console.log(res);
  //响应的状态码
  console.log(res.statusCode);
  //响应的数据
  //通过事件获取: 当有数据传输的时候，自动触发这个事件
  //使用回调函数来接收
  res.on('data',function(buf){
    console.log(buf.toString());
  });
});
```

- 创建web服务器  
  `var server=http.createServer()`  创建web服务器  
  `server.listen(8080)`  设置web服务器端口号，监听端口变化  
  `server.on('request', function(req,res){  })`  
   接收浏览器的请求，是一个事件，当有请求发生自动触发  
  - req  请求的对象  
    - url  请求的URL，显示端口后的部分  
    - method  请求的方法  
  - res  响应的对象  
    - writeHead(code, obj)  设置响应的状态码和头信息  
      - code状态  
      - obj是一个头信息的对象  
    - write()   设置响应的内容  
    - end()  结束响应，发送响应的内容到浏览器  

```js
//引入http模块
const http=require('http');
//创建web服务器
var server=http.createServer();
//设置web服务器的端口号，监听端口变化
server.listen(8080);

//接收浏览器的请求
//on 是一个事件，当有请求发生自动触发
//参数1: request 事件名称(请求)
//参数2: 通过回调函数来获取请求和做出响应
server.on('request',function(req,res){
  //req: 请求的对象
  //请求的URL
  console.log(req.url,req.method);
  //res: 响应的对象
  //设置响应的状态码和头信息
  /*
  res.writeHead(200,{
    Server:'server-name'
  });
  */
  //设置响应的状态码为302，跳转到其他URL
  res.writeHead(302,{
    Location:'http://www.baidu.com'
  });
  //设置响应的内容
  res.write('this is homepage');
  //结束响应，发送响应的内容到浏览器
  res.end();

  /*
  //判断请求的URL
  //根据请求的URL做出不同的响应
  if(req.url=='/login' && req.method=='GET'){
    res.write('login');
  }else if(req.url=='/study'){
    res.writeHead(302,{
    Location:'http://www.tmooc.cn'
  });
  }
  res.end()
  */
});
```

## express框架

>基于nodejs的，快速、开发、极简的web开发框架(非核心模块)

[链接 : express官网](www.expressjs.com.cn)  

  安装 :   `npm  install  express`  

`const express=require('express');`//引入express  
`var server=express();` //创建web服务器  
`server.listen(8080);` //设置端口  

```js
const express=require('express');
//引入查询字符串模块
const querystring=require('querystring');
//创建web服务器
var server=express();
//设置端口8080
server.listen(8080);
//路由
server.get('/reg',function(req,res){
  res.sendFile(__dirname+'/reg.html');
});
```

### 路由

>浏览器向web服务器发送请求，web服务器根据请求的方法和请求的URL来做出响应,
这个过程称为路由。

路由的三要素：**请求方法、请求的URL、响应（回调函数）**

- 请求的对象(req)
  - req.method  请求的方法
  - req.url  请求的URL
  - req.headers  请求的头信息
  - req.query  **获取请求时查询字符串传递的数据，并格式化为对象**
  - req.params **获取路由传参**
- 响应的对象(res)  
  - send('msg')   响应内容，只能响应一次
  - sendFile(path)  响应文件，**必须使用绝对路径( __dirname )**
  - redirect('url')  响应的重定向

```js
//路由
server.get('/reg',function(req,res){
  res.sendFile(__dirname+'/reg.html');
});
```

### post和get传递数据

- post请求是通过表单提交(暂时)传递数据，  
 服务器端是通过事件的形式获取数据(后期会有简单的方法:使用[第三方中间件](###中间件))  
req.on('data', function(buf){  
  buf就是获取的数据，格式为buffer，转为字符串后格式为查询字符串，需要借助查询字符串模块格式化为对象  
})  

```js
//根据表单的请求添加对应的路由
//post  /myreg
server.post('/myreg',function(req,res){
  //获取post请求传递的数据
  //以事件的形式
  //当有数据传输自动触发事件
  //使用回调函数接收数据  
  req.on('data',function(buf){
    //buf 传递的数据,是buffer形式
  //console.log(buf.toString());
  //查询字符串
  var str=buf.toString();
  //查询字符串(querystring)格式化为对象
  var obj=querystring.parse(str);
  console.log(obj);
  });

  res.send('注册成功');
});
```

- get请求以查询字符串形式传递数据，  
服务器端使用req.query获取数据，结果是对象。  
 查询字符串传递数据容易被浏览器所缓存，  
 而post传递数据不会出现在地址栏。  

```js
//根据表单的请求创建对应的路由
//get /mylogin
server.get('/mylogin',function(req,res){
  //获取get请求传递数据
  console.log(req.query);
  res.send('登录成功');
});
```

### 使用路由传递数据——路由传参

- 设置路由中接收的名称  

```js
//商品详情路由
server.get('/detail/:lid',function(req,res){
  //接收路由传递的数据
  console.log(req.params);
  res.send('商品详情');
});

//购物车路由
server.get('/shopping/:pname/:price',function(req,res){
  console.log(req.params);
  res.send('这是购物车');
});
```

- 接收路由传递的数据  
`req.params` 得到的数据是对象格式

- 浏览器传递参数  
 <http://127.0.0.1:8080/detail/5>  
 说明：5就是传递的数据，使用lid来接收  

### 路由器

>路由的使用过程中，不同的模块可能出现相同的URL，把同一个模块下的所有路由放到一个容器，这个容器就是路由器。  
>>路由器最终要引入到web服务器下才能使用。

- 创建路由器模块(自定义模块)  
`const express=require('express');`  
`var router=express.Router();  //创建路由器对象`  
`router.get('/list', function (req,res){  });//添加路由`  
`module.exports=router; //导出路由器对象`  

```js
//路由器文件中
//引入express
const express=require('express');
//使用express创建空的路由器
//返回对象
var router=express.Router();
//往路由器中添加路由
router.get('/list',function(req,res){
  res.send('这是商品模块下的列表');
});
//导出路由器对象
module.exports=router;
```

- 在web服务器下使用路由器  
`const productRouter=require('./product.js');`  
`server.use('/product', productRouter);//把路由器挂载到 /product 下`  
  **访问形式:**  /product/list  

```js
//服务器文件中
//引入商品路由器(自定义模块)
const productRouter=require('./product.js');

//商品模块路由
//使用商品路由器
//挂载到/product下
// /product/list
//参数1：挂载的位置
//参数2：使用的路由器
server.use('/product',productRouter);
```

### 中间件

>中间件理解是一个过滤器，作用是为主要的业务逻辑服务  
>>分为 : 应用级中间件、路由级中间件、内置中间件、第三方中间件、错误处理中间件

- 应用级(自定义)中间件  
  每个中间件都是一个函数  
  `server.use( path, function(req,res,next){  } )` ==> 过滤路由中url为path的路由  
  `server.use(function(req,res,next){  })` ==> 省略第一个参数,表示过滤所有的路由  

```js
//服务器中
const express=require('express');
var server=express();
server.listen(8080);
//使用中间件验证注册
//参数1: 给哪一个URL的路由使用；如果为空标识会给所有的路由使用
//参数2: 中间件函数；获取请求，以及做出响应
server.use('/reg',function(req,res,next){
  console.log('验证了数据是否为空');
  //会执行下一个中间件或者路由
  next();
});
server.use('/reg',function(req,res,next){
  //给url为/reg的路由添加前置的中间件，验证用户名是否可用
  //console.log('用户名可以使用');
  //next();
  console.log('该用户已被注册');
  res.send('请使用其它的用户名');
});
//主要的业务逻辑
server.get('/reg',function(req,res){
  res.send('注册成功');
});
server.get('/list',function(req,res){
  var num=3;
  res.send(num.toString());
});

/*=========================================================================*/

/*
创建路由(get , /view)响应当前的浏览次数；每次浏览次数加1。  
在中间件的外部声明变量初始化为0，在中间件中完成加1,在路由中把该变量响应到浏览器
*/
var n=0;
//添加中间件，给/view使用
server.use('/view',function(req,res,next){
  //n='1'
  n++;//++ 隐式将n转成数字
  next();
});
server.get('/view',function(req,res){
  res.send(n.toString());
});
```

- 路由级中间件  
   路由器的使用  
   `server.use(path, 路由器);`
- 内置中间件  
   在express4下只保留了一个内置的中间件  
   `server.use( express.static('目录') );`  
   把静态资源托管到指定的目录，如果浏览器请求静态资源，自动到该目录下查找。  
   静态资源：html、css、浏览器js、图像....  

```js
//服务器中
const express=require('express');
var server=express();
server.listen(8080);

//静态资源：html,css,浏览器端js,img...
//把所有的静态资源托管到public目录
//使用内置中间件static
server.use( express.static('public') );
server.use( express.static('files') );
//若两个静态资源托管文件夹中有同名文件，按托管顺序寻找，
//如：在'public'目录中找到了，就不会再去'files'目录中去寻找了
```

- 第三方中间件  
   `npm  install  中间件名称`  

使用中间件:  

```JS
 server.use( bodyParser.urlencoded({
   extended:false
 }) )
```

 urlencoded: 将post请求的数据格式化为对象  
 extended: 不是用第三方qs模块，而是使用核心模块querystrinig将查询字符串格式化为对象  

在路由中获取post请求数据 ==> req.body   格式为对象

```JS
const express=require('express');
//引入body-parser中间件
const bodyParser=require('body-parser');
//创建web服务器
var server=express();
server.listen(8080);
//托管静态资源到public目录
server.use( express.static('public') );
//使用body-parser中间件将post请求数据格式化为对象
server.use(bodyParser.urlencoded({
  extended:false  
  //不使用扩展的qs模块，而是使用querystring模块 格式化为对象
}));

//根据浏览器的请求写对应路由
server.post('/login',function(req,res){
  //获取post请求的数据，格式化为对象
  //前提：已经使用了中间件body-parser
  console.log(req.body);
  res.send('登录成功');
});
```

- 错误处理中间件  
 略……

## mysql模块

### mysql 语法

- 连接  mysql.exe -h127.0.0.1 -P3306 -uroot -p  
   简写 : mysql -uroot  
- 增  INSERT INTO emp VALUES(NULL, 'tom'...)
- 删  DELETE FROM emp WHERE uid=5;
- 改  UPDATE emp SET uname='jerry',salary=8000 WHERE uid=5;
- 查  SELECT * FROM emp;

### 使用mysql模块

- 连接mysql  
  - `var connection=mysql.createConnection();`  
   创建连接对象，传递连接数据库需要的服务器、端口、用户名、密码、要使用的数据库  
  - `connection.connect()`  
  建立连接  
  - `connection.query(sql, callback)`  
   sql是要执行的SQL语句，callback回调函数，用于获取SQL语句的结果  
  - `connection.end()`  
  执行完所有的SQL语句，关闭连接

```js
//引入mysql模块
const mysql=require('mysql');
//创建连接对象
var connection=mysql.createConnection({
  host:'127.0.0.1',
  port:'3306',
  user:'root',
  password:'',
  database:'tedu' //连接后使用的数据库
})
//建立连接
connection.connect();
//执行SQL语句
//参数1: SQL语句
//参数2: 回调函数，用于获取SQL语句的结果
/*
connection.query('SELECT * FROM emp',function(err,result){
   //err可能产生的错误
   if(err) throw err;
   //result 执行的结果
   console.log(result);
});
*/
//使用mysql模块删除员工表emp中编号为5的数据，打印结果
connection.query('DELETE FROM emp WHERE eid=6',function(err,result){
  if(err) throw err;
  //console.log(result);
  if(result.affectedRows>0){
    console.log('删除成功');
  }else{
    console.log('删除失败');
  }
});
//关闭连接
connection.end();
```

- 连接池  
  - `var pool=mysql.createPool();`  
  创建连接池对象，传递连接需要的服务器地址、端口、用户名、密码、要使用数据库、设置连接池的大小 `connectionLimit`，默认是15
  - `pool.query(sql, callback)`  
  执行SQL语句

```js
//引入mysql
const mysql=require('mysql');
//创建连接池对象，自动建立连接
var pool=mysql.createPool({
  host:'127.0.0.1',
  port:'3306',
  user:'root',
  password:'',
  database:'tedu',
  connectionLimit:20  //设置连接池的大小
});
//执行SQL语句
/*
pool.query('SELECT * FROM emp',function(err,result){
  if(err) throw err;
  console.log(result);
});

//往部门表中插入数据，查看结果
//var did=18;
//var dname='安保部';
// ?占位符, 防止SQL注入攻击数据库
pool.query('INSERT INTO dept VALUES(?,?)',[did,dname],function(err,result){
  if(err) throw err;
  console.log(result);
});

var obj={
  did:14,
  dname:'后勤部'
}
pool.query('INSERT INTO dept VALUES(?,?)',[obj.did,obj.dname],function(err,result){
  if(err) throw err;
  console.log(result);
})

var obj={
  did:21,
  dname:'财务部'
}
pool.query('INSERT INTO dept SET ?',[obj],function(err,result){
  if(err) throw err;
  console.log(result);
});
*/
//将部门表dept中编号为40的数据，部门名称改为“测试1部”
pool.query('UPDATE dept SET dname=? WHERE did=?',['测试1部',40],function(err,result){
  if(err) throw err;
  console.log(result);
});
```
