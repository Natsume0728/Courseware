# diff 命令相关

- `git diff`  
使用前提：文件已add到暂存区后又做了修改；  
使用此命令可以在默认编辑器中查看修改后的当前文档与暂存区中的此文档的差异；  
如果暂存区没有文件，将会与commit后即本地仓库种的文件进行比较；  
- `git diff --cached`  
使用前提：文件之前commit过，修改此文件且add到暂存区；
使用带参数 --cached 的diff命令，可以在默认编辑器中查看修改后add到暂存区的文件与之前commit版本的差异；

tips：  
diff 命令为使用git默认的比较工具进行比较，diff 可以换成difftool,使用设定的编辑工具进行比较(个人设置为vscode)；  
即上述两个命令可以修改为：  
`gti difftool`和`git difftool --cached`;  
使用设定的比较工具vscode进行比较；
