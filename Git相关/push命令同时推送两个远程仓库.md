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

tips：  
实际使用时，可以根据需要添加不止两个仓库，  
但是，如果其中一个仓库链接超时，会导致任何一个仓库的推送都不成功；  
比如：以github为代表的远程仓库，现在是凌晨三点竟然链接超时！！！

github链接超时，导致gitee的push也未成功，但是gitee貌似有响应消息：  
gitee似乎响应回了"Bye Bye"???如下：  

```git
Administrator@PC-201906172306 MINGW32 /f/markdown (dev)
$ git push origin dev
Received disconnect from 52.74.223.119 port 22:11: Bye Bye
Disconnected from 52.74.223.119 port 22
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

同时push成功：

```git
Administrator@PC-201906172306 MINGW32 /f/markdown (dev)
$ git push origin dev
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 4 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 904 bytes | 904.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:Natsume0728/markdown.git
   ae79b93..522b7d4  dev -> dev
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 4 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 904 bytes | 904.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0)
remote: Powered By Gitee.com
To gitee.com:natsume0728/markdown.git
   ae79b93..522b7d4  dev -> dev
```
