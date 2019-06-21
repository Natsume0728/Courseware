# git

## git clone

- `git clone url`  
在本地生成一个目录，与远程仓库的版本库同名；  
- `git clone url <本地目录名>`  
clone同时指定生成的目录名称(即可与远程不同名)  
- `git clone -o name url`  
克隆时添加 -o 参数，可以设定远程仓库的名称；  
(因为克隆远程库的时候，远程库自动被命名为origin，如果需要自定义名称时可以使用此命令，在有多个远程库的情况下比较好用)；  

## git remote

- `git remote`  
不带参数会列出所有的远程仓库；  
- `git remote -v`  
添加 -v 参数，可以查看远程仓库的URL；
- `git clone -o name url`  
克隆时添加 -o 参数，可以设定远程仓库的名称；  
(因为克隆远程库的时候，远程库自动被命名为origin)；  
- `git remote show <远程库名称>`  
查看远程库的详细信息；  
- `git remote add <自定义远程库名> url`  
添加远程库；  
- `git remote rm <远程库名>`  
删除远程库；  
- `git rename <old name> <new name>`  
重命名远程库；  

## git fetch

>一旦远程仓库有了更新(commit),需要将这些更新取回本地，可以使用 git fetch 命令，通常用来查看他人进程；  
默认情况下 git fetch 取回所有分支的更新；  

- `git fetch <远程库名称>`  
将远程库的更新全部取回本地；  
- `git fetch <远程库名称> <远程分支名>`  
因为 git fetch 命令默认取回所有分支的更新，  
若只想取回特定分支的更新，可以指定分支名称；  
所取回的更新，在本地主机上要用"远程主机名/分支名"的形式读取；  
比如origin仓库的master分支，就要用origin/master读取。  
- `git branch -r/-a`  
git branch 命令的 -r 参数可以查看远程分支；  
-a 参数查看所有分支；
- `git checkout -b new_branch origin/master`  
在fetch(取回远程库更新)后，在origin/master的基础上使用checkout命令创建一个新的分支；  
- `git merge origin/master` OR `git rebase origin/master`  
在fetch后，也可以使用merge或者rebase命令，在当前分支上合并远程分支；  

## git pull

>git pull命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并。  

- `git pull origin <远程分支名>：<本地分支名>`  
取回远程库的指定分支与本地指定分支合并；  
- `git pull origin <远程分支名>`  
如果要取回的远程库的指定分支与当前分支合并，可省略<本地分支名>  
等同于，先git fetch 再 git merge ；  
- `git branch --set-upstream <本地分支名> origin/<远程分支名>`  
指定本地分支追踪(tracking)远程库特定分支；  
在git clone 时，本地master分支自动追踪origin/master分支；  
- `git pull origin`  
如果当前分支与远程库的分支存在追踪关系，命令中可以省略远程分支名；  
上述命令表示：  
本地的当前分支自动与对应的origin主机"追踪分支"（remote-tracking branch）进行合并。  
- `git pull`  
如果当前分支只有一个追踪分支，连远程主机名都可以省略。  
上面命令表示，当前分支自动与 __唯一一个追踪分支__ 进行合并。  
- `git pull --rebase <远程仓库名> <远程分支名>:<本地分支名>`  
如果合并需要采用rebase模式，可以使用--rebase参数；  
- `git pull -p`  
如果远程主机删除了某个分支，默认情况下，git pull 不会在拉取远程分支的时候，删除对应的本地分支。  
这是为了防止，由于其他人操作了远程主机，导致git pull不知不觉删除了本地分支。  
但是，可以改变这个行为，加上参数 -p 就会在本地删除远程已经删除的分支。  

## git push  

- `git push <远程主机名> <本地分支名>:<远程分支名>`  
将本地分支的更新，推送到远程主机。  
__注意，分支推送顺序的写法是<来源地>:<目的地>，所以git pull是<远程分支>:<本地分支>，而git push是<本地分支>:<远程分支>。__
- `git push origin master`  
省略远程分支名，则表示将本地分支推送与之存在"追踪关系"的远程分支（通常两者同名），  
__如果该远程分支不存在，则会被新建。__  
- `git push origin :master`  
__省略本地分支名，则表示删除指定的远程分支__，因为这等同于推送一个空的本地分支到远程分支。  
- `git push origin`  
当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。  
- `git push`  
如果当前分支 __只有一个追踪分支__ ，那么主机名都可以省略。  
- `git push -u origin master`  
如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push。  
- `git config --global push.default matching`  
OR  
`git config --global push.default simple`  
不带任何参数的git push，默认只推送当前分支，这叫做simple方式。  
此外，还有一种matching方式，会推送所有有对应的远程分支的本地分支。  
Git 2.0版本之前，默认采用matching方法，现在改为默认采用simple方式。  
如果要修改这个设置，可以采用上述git config命令。  
- `git push --all origin`  
不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要使用--all选项。
- `git push --force origin`  
如果远程主机的版本比本地版本更新，推送时Git会报错，要求先在本地做git pull合并差异，然后再推送到远程主机。  
这时，如果你一定要推送，可以使用--force选项。  
结果会导致远程主机上更新的版本被覆盖。除非你很确定要这样做，否则应该尽量避免使用--force选项。  
- `git push origin --tags`  
git push不会推送标签（tag），除非使用--tags选项。  
