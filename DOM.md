# DOM

## 查找元素(4种)

1. 不需要查找就可以直接获得的元素
   - document:    根节点对象
   - \<html>根元素:    document.documentElement
   - \<head>元素:    document.head
   - \<body>元素:    document.body
1. 按节点间关系查找  
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

1. 按HTML特征查找
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
