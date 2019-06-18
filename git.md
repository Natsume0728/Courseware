# A note for learn git  

## ERRORS  

- `Please enter a commit message to explain why this merge is necessary.`  
    git 在pull或者合并分支的时候有时会遇到这个界面。  
    基本原因是因为本地库的代码跟远程库有冲突需要合并,  
    处理方法  
    1. 按键盘字母 i 进入insert(输入)模式,编辑必要的注释 说明合并的原因,编辑的内容会在第一行显示,也可不修改  
    1. 修改最上面那行黄色合并信息,可以不修改  
    1. 按"Esc"  
    1. 输入":wq",按回车键即可  

- >ssh: connect to host github.com port 22: Connection timed out
fatal: Could not read from remote repository.
Please make sure you have the correct access rights
and the repository exists.

  >利用ssh 及命令`git clone...`下载GitHub上的仓库报上述错误，且ssh公钥 已在GitHub保存，经 {==`ssh -T git@github.com`==}测试ssh是否配置成功，同样报`ssh: connect to host github.com port 22:Connection timed out`错误，错误提示中有`22 端口`，暂未找到端口相关解决方式，可行解决方式：`Clone with HTTP`,命令`git clone https://github.com/ Natsume0728/markdown.git`即可正常下载。

- >Administrator@PC-201906172306 MINGW32 /f/markdown (master)
$ git pull
fatal: refusing to merge unrelated histories//拒绝合并不相关历史

 本地仓库不是从远程仓库clone来，执行pull操作时会出现此错误，本质上是因为本地仓库和远程仓库是两个独立的不相关仓库。  
 加上-allow-unrelated-histories参数可解决。  
`$git pull origin master –allow-unrelated-histories`

## git文件状态`git status`  

1. 在本地git仓库中新建 `001.html`文件 `002`目录  
![Untracked files](./img/git_001.jpg)  
文件001.html状态为:__Untracked files__(未监视)  
若新建目录为空，`git.status`命令不会将这个目录显示在`Untracked files`中。  
1. `git add [filename]or[dirname/]`后文件状态：__Changes to be committed,绿色字体显示new file__:  
![changes to be committed](./img/git_002.jpg)  
1. 修改文件001.html中的内容后执行`git status`命令，001.html文件状态为：__Changes not staged for commit__(文件已执行过`add`操作，理解为已纳入跟踪后做了修改，而未将修改后的文件提交到缓存区)，__红色字体显示modified__  
![changes to be committed](./img/git_003.jpg)  
1. commit操作后  
![changes to be committed](./img/git_004.jpg)  
1. commit操作后再次修改文件内容  
![changes to be committed](./img/git_005.jpg)  
同样显示 __Changes not staged for commit状态，同样标为红色modified__。  

## git命令（含Linux命令）  

- `ssh-keygen -t rsa -C <email>`创建SSH KEY  
- `mkdir <dir>`创建目录(Linux)  
- `cd <dirn>`进入目录(Linux)  
- `pwd`显示当前目录  
- `vim <file>`在编辑器中修改文件内容  
  - __i__ 插入(进入编辑器编辑文件)  
  - __Ese__ 退出编辑器  
  - __:wq__ 保存并退出  

***

- `git init`将当前仓库变成Git可以管理的本地仓库  
- `git add <file>or<dir/>`  
- `git status`查看文件状态，冲突文件  
- `git commit -m <message>`  
- `git config [--global][--system] user.email '...'`引号可省略  
- `git config [--global][--system] user.name '...'`引号可省略  

***

[远程仓库的使用](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8)  

- `git remote add <远程仓库的本地名称> url`  
- `git clone url`克隆远程仓库，__该命令不要求在`init`后的目录中使用，本地非git初始化目录也可使用，克隆完项目后会有一个默认名为origin的远程库__。  
- `git remote`列出每个远程库的简短名字。  
- `git remote -v`显示对应的克隆地址。  
- `git remote show [remote-name]`查看远程仓库的详细信息。  
- `git remote add [shortname][url]`添加远程库  
- `git remote rename [old_name][new_name]`修改远程仓库的本地简称。  
- `git remote rm [remote_name]`移除远端仓库。  

***
Git push  
在使用git commit命令将修改从暂存区提交到本地版本库后，只剩下最后一步将本地版本库的分支推送到远程服务器上对应的分支。  

- `git push origin [local_branch_name]:[remote_branch_name]`把本地分支locan_branch_name推送到远程库，并在远程库中新建名为[remote_branch_name]的分支。  
- `git push origin [branch_name]`远程分支被省略，将本地分支推送到与之存在追踪关系的远程分支（通常两者同名），如果该远程分支不存在，则会被新建。  
- `git push origin` 如果当前分支与远程分支存在追踪关系，则本地分支和远程分支都可以省略，将当前分支推送到origin主机的对应分支  
- `git push -u origin master`如果当前分支与多个主机存在追踪关系，则可以使用 -u 参数指定一个默认主机，这样后面就可以不加任何参数使用git push，不带任何参数的git push，默认只推送当前分支，这叫做 __simple方式__，还有一种 __matching方式__，会推送所有有对应的远程分支的本地分支， Git 2.0之前默认使用matching，现在改为simple方式如果想更改设置，可以使用git config命令。git config --global push.default matching OR git config --global push.default simple；可以使用git config -l 查看配置
- `git push --all origin`当遇到这种情况就是不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要 -all 选项。  
- `git push --force origin git push`的时候需要本地先git pull更新到跟服务器版本一致，如果本地版本库比远程服务器上的低，那么一般会提示你git pull更新，如果一定要提交，那么可以使用这个命令。
- `git push [远程名]:[分支名]`删除远程分支

***

- `git checkout -b dev`创建并切换到新分支dev
- `git branch dev`创建新分支dev
- `git checkout dev`切换到新分支
- `git branch`查看当前所有分支
- `git branch -v`查看各个分支最后一个提交对象的信息
- `git branch --merged`查看哪些分支已被并入当前分支(即是当前分支的直接上游分支。)
- `git branch --no-merged`查看尚未合并分支
- `git merge dev`合并指定分支(dev)到当前分支
- `git branch -d dev`删除分支dev
- `git branch -D dev`强制删除分支(若所删除分支中包含未合并信息，需要用参数-D强制删除)
- `git log --graph`git点线树  
![git log --graph](./img/git_006.jpg)  
  - `git log --graph --pretty=oneline`git点线树单行显示，__commit id完整显示__。
![--pretty=oneline](./img/git_007.jpg)  
  - `git log --graph --oneline`git点线树单行显示，__commit id简写__。  
![--pretty=oneline](./img/git_008.jpg)
  - `git log --graph --oneline --all`__增加参数`--all`可显示所有分支的点线树__。
  - `gitk`内置图形化工具，`git log`命令的可视化版本  ，同样可以加 __参数`--all`__。
[git log命令的详细介绍](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2)  

***
tag

- `git tag`查看所有标签。
- `git tag <tagname> [commit id]`用于新建一个标签，默认为HEAD,也可以指定一个commit id
- `git tag -a <tagname> -m [message]`指定标签信息
- `git tag -d <tagname>`删除一个本地标签
- `git push origin <tagname>`推送一个本地标签
- `git push origin --tags`推送全部未推送过的本地标签
- `git push origin :refs/tags/<tagname>`删除一个远程标签

***

tips：

- git fetch 和 git pull 的差别
  git fetch 相当于是从远程获取最新到本地，不会自动merge  

  >git fetch github master//将远程仓库github的master分支下载到本地当前branch中
git log -p master ..github/master//比较本地master分支和远程仓库master分支的差别
git merge github/master//进行合并

  类似指令  
  >git fetch github master:tmp//从远程仓库master分支获取最新，并在本地建立tep分支
git diff tmp//将当前分支和tmp进行对比
git merge tmp//合并tmp分支到当前分支
  
  git pull 相当于是从远程获取最新版本并merge到本地：  
  `git pull github master`  
  __在实际使用中，git fetch 更安全一些。__  
