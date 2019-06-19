# …rest

>代替arguments使用
arguments为类数组对象，数组的方法不能使用；
只能获得全部参数，不能有选择的获得部分实参值

Ex：  
定义一个函数，并且不指定输入项的大小，并进行求和操作。  

```html
<script>
    var arr = [12, 32, 22]
    function add(...rest) {
        let sum = 0;
        for (var val of rest) {
            sum += val;
    }
    console.log(sum);
    }
    add(...arr)
</script>
```

[参考链接](https://www.jianshu.com/p/a39bee665233)
