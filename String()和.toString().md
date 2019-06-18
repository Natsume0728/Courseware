# String( ) / .toString( )

- __toString()__ 可以将所有的的数据都转换为字符串，但是要排除null 和 undefined

例如将false转为字符串类型  

```html
1   <script>
2       var str = false.toString();
3       console.log(str, typeof str);
4   </script>
```

返回的结果为 false，string  

看看null 和 undefined能不能转换为字符串  

```html
1   <script>
2       var str = null.toString();
3       console.log(str, typeof str);
4   </script>
```

结果程序报错

```html
1   <script>
2       var str = undefined.toString();
3       console.log(str, typeof str);
4   </script>
```

程序也报错
***

__.toString()__ 括号中的可以写一个数字，代表进制，对应进制字符串
>二进制：.toString(2);  
八进制：.toString(8);
十进制：.toString(10);
十六进制：.toString(16);

- __String()__ 可以将null和undefined转换为字符串，但是没法转进制字符串
例如将null转换为字符串  

```html
1   <script>
2       var str = String(null);
3       console.log(str, typeof str);
4   </script>
```

返回的结果为 null，string  

将undefined转换为字符串  

```html
1   <script>
2       var str = String(undefined);
3       console.log(str, typeof str);
4   </script>
```

返回的结果为 undefined，string  

[参考链接](https://www.cnblogs.com/good10000/p/6004459.html)  
