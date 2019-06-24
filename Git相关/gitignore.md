# .gitignore的配置  

- 常见忽略规则  

```git
1 node_modules    忽略node_modules的单文件  
2  
3 *.zip            表示忽略所有 .zip结尾的文件
4  
5  /dist          忽略项目根目录下的 dist 文件夹,但不包括子目录下的dist文件夹
6  
7  build/          忽略 build/目录下的所有文件，包括子目录下的文件
```

- 对应IDE及开发项目的.gitignore文件。  
常用生成网站 <https://www.gitignore.io/> 。  
- 执行下面命令可以解决 .gitignore 不生效问题。

```git
git rm -r –-cached .
git add .  
git commit -m "update gitignore"  
```
