# git中分支合并Fast-forward和--no-ff模式  

- Fast-forward 快进模式  
  1. 在master分支上新建文件001.html后commit。  
  1. 新建并转到dev分支，`git checkout -b dev`。  
  1. 在dev分支上新建文件002.html后commit。  
  1. 转回master并合并分支dev，`git merge dev`。  
![git_009.png](https://i.loli.net/2019/06/19/5d09c814c8c2078290.png)  
git点线树显示如下`git log --graph --oneline`：  
![git_010.jpg](https://i.loli.net/2019/06/19/5d09c814cc73881686.jpg)  
gitk工具显示如下：  
![git_011.jpg](https://i.loli.net/2019/06/19/5d09c8a99f53e91044.jpg)  

- --no-ff 禁用快进模式  
  1. 新建并转到dev2分支，`git checkout -b dev2`。  
  1. 在dev2分支上新建文件003.html后commit。  
  1. 转回master并使用--no-ff模式合并分支dev2，`git merge --no-ff -m <message> dev2`  
![git_012.jpg](https://i.loli.net/2019/06/19/5d09c8a9a36af78824.jpg)  
git点线树显示如下`git log --graph --oneline`：  
![git_013.jpg](https://i.loli.net/2019/06/19/5d09c8aa3cef629788.jpg)  
gitk工具显示如下：  
![git_014.jpg](https://i.loli.net/2019/06/19/5d09c8aa0713092709.jpg)  

***

tip:  

- 快进模式合并分支命令`git merge dev`,git是把`master`指向`dev`当前的commit(且可以看出此种模式的merge并没有产生新的commit)就完成了合并，所以速度很快，但是有缺点，删除分支后，会丢掉分支信息，==后期从分支历史上看不出曾经做过合并==;  
- 禁用快进模式合并分支命令`git merge --no-ff -m <message> dev2`，此种模式git会在merge时生成一个新的commit(所以需要-m参数),这样，__删除分支后，从分支历史上仍可以看出曾经做过合并__。  
git点线树和gitk工具显示如下：  
![git_015.jpg](https://i.loli.net/2019/06/19/5d09c8a9b600a92263.jpg)  
![git_016.jpg](https://i.loli.net/2019/06/19/5d09c8a9a162879558.jpg)  
