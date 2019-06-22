# 配置VS code为git的默认编辑器，difftool及mergetool

- 直接修改 .config 文件  
编辑器在[core]中修改,前提是VS code的路径已加到环境变量PATH中；  
合并和比较工具分别在[diff],[difftool],[merge],[mergetool]中修改；

```git
[color]
	ui = true
[gui]
	recentrepo = D:/natsume
[core]
	editor = code --wait
[user]
	name = natsume
	email = 1047743906@qq.com
[diff]
	tool = vscode
[difftool "vscode"]
	cmd = "code --wait --diff $LOCAL $REMOTE"
[merge]
    tool = vscode
[mergetool "vscode"]
	cmd = "code --wait $MERGED"
```

- 命令行修改
  - 编辑器：  
  前提还是VS code的路径已加到环境变量PATH中；  
`git config --global core.editor "code --wait"`
  - 合并工具(mergetool)：  
  `git config --global merge.tool vscode`  
`git config --global mergetool.vscode.cmd "code --wait $MERGED"`  
  - 比较工具(difftool)：  
`git config --global diff.tool vscode`  
`git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"`  

ps:环境变量的配置  
![环境变量1.png](https://i.loli.net/2019/06/22/5d0e2fca9135548201.png)  
![环境变量2.png](https://i.loli.net/2019/06/22/5d0e2fbf5b3f297448.png)  
