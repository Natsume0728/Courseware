# HTTP协议

<!-- TOC depthFrom:2 orderedList:false -->

- [HTTP协议](#http%e5%8d%8f%e8%ae%ae)
  - [URL](#url)
  - [http协议](#http%e5%8d%8f%e8%ae%ae)
  - [web请求原理详解](#web%e8%af%b7%e6%b1%82%e5%8e%9f%e7%90%86%e8%af%a6%e8%a7%a3)
  - [消息/报文 Message](#%e6%b6%88%e6%81%af%e6%8a%a5%e6%96%87-message)
  - [Request Message](#request-message)
  - [Response Message](#response-message)
  - [缓存](#%e7%bc%93%e5%ad%98)
  - [HTTP性能优化](#http%e6%80%a7%e8%83%bd%e4%bc%98%e5%8c%96)
  - [安全HTTP协议:https](#%e5%ae%89%e5%85%a8http%e5%8d%8f%e8%ae%aehttps)

<!-- /TOC -->

## URL

结构：  
协议+主机名称+目录结构+文件名称

URL完整的结构：
\<scheme>://\<user>:\<pwd>@\<host>:\<port>/\<path>;\<params>?\<query>#\<frag>

- scheme：  方案，协议。设置以哪种方式获取服务器资源
  协议是不区分大小写的，常用的协议http:/ftp：
![协议及端口号.png](https://i.loli.net/2019/07/04/5d1db7bcc1e8c85165.png)
- \<user>:\<pwd>  用户名：密码。此种写法已过时。
- \<host>  主机名 (域名、ip地址)
- \<port>  端口号  
- \<path> 资源，在服务器上具体存放的位置
- \<params>  参数，保存跟踪状态的参数(session/cookie)
- \<query> get方法提交请求时的查询字符串
- #\<frag> 锚点

---

## http协议

>HTTP:HyperText Transfer Protocol 超文本传输协议
规范了数据是如何打包以及传递的
(专门用于传输html文件的协议，专门浏览网页的协议)

HTTP协议的历史:
![HTTP协议历史.png](https://i.loli.net/2019/07/04/5d1db80a19b1675154.png)

---

## web请求原理详解

![请求响应流程.png](https://i.loli.net/2019/07/04/5d1db8a100f9794544.png)
[视频：web请求原理详解P-1](https://www.bilibili.com/video/av57824059/?p=1)
[视频：web请求原理详解P-2](https://www.bilibili.com/video/av57824059/?p=2)

---

## 消息/报文 Message

![message.png](https://i.loli.net/2019/07/04/5d1db8e0d587c98073.png)

- 请求消息 Request Message(请求起始行，请求头，请求主体)
- 响应消息 Response Message(响应起始行，响应头，响应主体)

---

## Request Message

>请求消息，客户端发送给服务器的数据块;
由三部分组成，请求起始行，请求头，请求主体

- 请求起始行
    1. 请求方法
        - get:明文提交，不安全，有大小限制 2kb
      客户端向服务器要数据的时候使用get
      靠地址栏传递查询字符串的方式传数据，
      无请求主体
        - post:隐式提交，无大小限制
       客户端要传递数据给服务器时使用。
       有请求主体，靠请求主体传递数据
        - delete:客户端想要删除服务器上的内容(一般禁用)
        - put：客户端想往服务器上放文件内容(一般禁用)
        - connect:测试连接
        - trace：追踪请求路径
        - option 预请求
        - head：表示客户端只获取响应消息头
    1. 协议版本号 HTTP/1.1
    1. 请求的url

- 请求头
    1. `host：www.tmooc.cn`
告诉服务器请求的是哪一个主机
    1. Connection:keep-alive
告诉服务器开启持久连接
    1. User-Agent：告诉服务器，浏览器的类型和浏览器版本号
    1. Accept-Encoding:gzip
告诉服务器，我这个浏览器可以接收的压缩文件的格式
    1. Accept-Language:zh-CN
告诉服务器，我这个浏览器可以接收的自然语言的类型
    1. Referer: `http://www.tmooc.cn/free/`
告诉服务器，当前请求来自于哪个网页s

- 请求主体
form data
get请求没有请求主体
post有请求主体

---

## Response Message

>响应消息，服务器发送给客户端的数据块
由三部分组成：响应起始行，响应头，响应主体

- 响应起始行
    1. 协议版本 http/1.1
    2. 响应状态码:告诉浏览器，服务器的响应状态是什么
        - 1XX 正在请求，提示信息
        - 2XX  
              - 200 响应成功
        - 3XX  重定向  
              - 301 永久重定向
              - 302 临时重定向
              - 304 同一个请求，没有任何变
                      命中缓存
        - 4XX  
              - 404 请求资源不存在
              - 403 权限不够
              - 405 请求方法不被允许
        - 5XX  
              - 500服务器代码错误
    3. 原因短句(对响应状态码的简短解释)

- 响应头
    1. Date:Sun, 05 May 2019 08:19:02 GMT
告诉浏览器，服务器响应的时间，格林威治时间
    1. Connection:keep-alive
告诉浏览器，服务器已经开启了持久连接
    1. Content-Type:
告诉浏览器，响应主体的类型是什么
  取值:
        - text/html 响应回来的数据是html文本
        - text/css   响应回来的数据是css文本
        - application/JavaScript  是js文本
        - image/jpg gif png  响应回来的是图片
        - text/plain 响应回来的是普通文本
        - application/json响应回来的是json字符串
        - application/xml 响应回来的是xml字符串

- 响应主体
服务器传递给浏览器的数据

---

## 缓存

>客户端经服务器响应回来的数据进行自动的保存
当再次访问的时候(请求不改变)，直接使用保存的数据

![缓存.jpg](https://i.loli.net/2019/07/04/5d1dbc9696a1c69872.jpg)

- 缓存的优点：
    1. 减少冗rong余的数据传输，节省客户端流量
    2. 节省服务器带宽
    3. 降低了对服务器资源的消耗和运行的要求
    4. 降低了由于远距离传输而造成加载延迟  

- 缓存的新鲜度和过期  
![缓存流程.png](https://i.loli.net/2019/07/04/5d1dbcd985b1d10557.png)
  - 请求--无缓存--连接服务器--存缓存--客户端得到数据
  - 请求--有缓存--够新鲜--使用缓存--客户端得到
  - 请求--有缓存--不新鲜--连接服务器确认是否过期--没过期--更新缓存的新鲜度--客户端得到数据
  - 请求--有缓存--不新鲜--连接服务器确认是否过期--已过期--连接服务器拿数据--存缓存--客户端得到数据

- 与缓存相关的消息头
Cache-Control:max-age=0
从服务器将响应传到客户端之时起，此数据处于新鲜的秒数，这是一个相对时间
语法：Cache-Control:max-age=3600

- 在网页中添加缓存，需要修改消息头
\<meta http-equiv="消息头属性" content="值">
\<meta http-equiv="Cache-Control"  
content="max-age=3600">

---

## HTTP性能优化

- HTTP的连接过程
发起请求-->建立连接-->服务器处理请求-->访问资源-->构建响应-->发送响应-->记录日志

- HTTP连接性能优化
  1. 减少连接的创建次数(开启持久连接)
  2. 减少请求的次数（整合代码，不要让文件过多）
  3. 提高服务器端运行速度
  4. 尽可能的减少响应数据的长度

---

## 安全HTTP协议:https

HTTPS：安全版本的http协议
SSL：为数据通信特供安全支持

- 客户端发送请求--->ssl层加密-->服务器接收到加密文件-->ssl层解密，得到明文
- 服务器发送响应--->ssl层加密-->客户端得到加密文件-->ssl层解密，得到响应内容
