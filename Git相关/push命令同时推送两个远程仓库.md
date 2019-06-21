# 使用一条git push命令同时推送两个远程仓库

`git remote set-url --add oginin [url]`  
使用词条命令相当于在之前的远程仓库origin下新增了一个推送地址；  
运行git remote -v 命令后可看到origin仓库的push地址有两个了；  
个人理解为同名的两个不同的远程仓库。

```git
Administrator@PC-201906172306 MINGW32 /f/markdown (dev)
$ git remote -v
origin  git@github.com:Natsume0728/markdown.git (fetch)
origin  git@github.com:Natsume0728/markdown.git (push)
origin  git@gitee.com:natsume0728/markdown.git (push)
```

直接修改项目目录中的 .git/config文件与上述命令效果相同(不推荐)  

```git
[remote "origin"]
    url = git@github.com:Natsume0728/markdown.git
    fetch = +refs/heads/*:refs/remotes/origin/*
    url = git@gitee.com:natsume0728/markdown.git
```
