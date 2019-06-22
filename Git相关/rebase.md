# rebase

在dev分支上有4次新的commit

![rebase_001](http://wx3.sinaimg.cn/mw690/007hvodfgy1g4ajgrrk94j30cv03zq2v.jpg)  
需求：将最后三次commit合并为一次

命令`$ git rebase -i 7e8dda4`  
完整命令应该是：`git rebase -i  [startpoint]  [endpoint]`  
如果不指定endpoint，默认为HEAD的指向commit；  
注意：操作的区间并不包含[startpoint]  
也可以使用`$ git rebase -i HEAD~3`来划定区间为从HEAD指向的commit向前的3次commit(包含HEAD指向commit的三次commit)  
确认命令后进入如下编辑器界面  
![rebase_002](http://wx1.sinaimg.cn/small/007hvodfgy1g4ajq2c186j30h10frwf9.jpg)  
上面未被注释的部分列出的是本次rebase操作包含的所有提交，  
下面注释部分是git提供的命令说明。  
每一个commit id 前面的pick表示指令类型。  

- pick：保留该commit（缩写:p）
- reword：保留该commit，但需要修改该commit的注释（缩写:r）
- edit：保留该commit, 但是停下来修改该提交(不仅仅修改注释)（缩写:e）
- squash：将该commit和前一个commit合并（缩写:s）
- fixup：将该commit和前一个commit合并，不保留该提交的注释信息（缩写:f）
- exec：执行shell命令（缩写:x）
- drop：丢弃该commit（缩写:d）  

使用s(quash)指令修改commit内容，合并最后三次提交（将第2和第3行的pick修改为s）  保存后会再次进入编辑器，修改合并commit的注释信息，保存退出即可；  
![rebase_003](http://wx1.sinaimg.cn/small/007hvodfgy1g4ajt4jiiwj30fa0gct93.jpg)  
查看结果，如下所示：  
![rebase_004](http://wx4.sinaimg.cn/small/007hvodfgy1g4ajvlj8xjj30ch03cmx2.jpg)  
另：从git log中可看出合并后的提交会有一个新的commit id。  
使用reset命令结合reglog还是可以回滚到合并提交前的状态。  
