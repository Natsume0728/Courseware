# RegExp对象  

 什么是: 保存一条正则表达式，并包含用正则表达式执行验证和查找功能 的对象  
 何时: 只要在js中使用正则表达式，都要先创建正则表达式对象，再使用正则。  
 如何:  

- 创建正则表达式对象: 2种方式  

1. 创建一个固定的正则表达式对象:  
 var reg= /正则/ig  
 问题: //之间不允许写js语句动态生成正则表达式  
1. 正则表达式需要动态生成  
 var reg=new RegExp("正则","ig")  
 说明: 因为RegExp的第一个形参要求接受一个字符串格式的正则表达式。  
 所以，有无数种办法，拼接出我们想要的任何字符串。  
 比如:  
 var str=kwords.join("|");  
      "明月|白鹭"  
    var reg=new RegExp(str);  
      /明月|白鹭/  

- RegExp对象中包含两个函数:__test__ &nbsp; __exec__ ；  

1. 验证字符串是否符合格式要求：test  
      var bool=reg.test(str)  
       用正则表达式reg，检查str字符串是否符合格式要求  
       返回值: true/false  
      坑: test()默认只要能找到符合条件的部分内容，就返回true  
      解决: 今后凡是验证，都必须前加^，同时后加$  
      比如: //定义手机号的规则表达式reg  
        var reg=/^1[3-9]\d{9}$/;  
        //用规则表达式去验证手机号是否符合格式要求  
        var result=reg.test(phone);  
        //如果符合要求  
        if(result==true){  
           ... ...  
1. 第四种查找: 查找所有敏感词的内容和位置exec  
  var arr=reg.exec(str)  
   在字符串str中查找一个符合正则表达式reg要求的关键词  
   返回值: 跟str.match(reg)不加g，返回的值完全相同  
     arr [ 0: 关键词内容, index: 关键词的位置i ]  
   问题：每次只返回一个敏感词的内容和位置  
   解决：只要反复调用，reg.exec()会自动跳到下一个继续查找  
   找所有：用循环  
   var reg=/小[\u4e00-\u9fa5]/g;  
    do{//反复do  
        //查找敏感词  
        var arr=reg.exec(str);  
        //如果找到敏感词，才输出  
        if(arr!=null){  
            console.log("找到敏感词!");  
            console.log(arr);  
        }else{//否则(找不到)，就退出循环  
            console.log("找不到了，就退出！")  
            break;  
        }  
    }while(true);  
    //true 不使用循环条件控制退出，因为我也不知道循环几次！  
    //而是在循环体内根据条件，用break随时可能退出循环。  
