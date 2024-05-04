### Git

> 分布式版本控制工具,相比集中式版本控制工具--在自己的主机中有所有的版本历史记录
>
> git中有工作区，暂存区，本地库和远程库
>
> git追踪的是修改而非文件(若对文件执行了修改而没有add到暂存区，则执行commit之后该修改不会被提交到本地库)

### 基础命令

1. `git init` 初始化本地库，将当前目录变成git可以管理的仓库
2. `git add <file>`可以一次添加多个文件到暂存区
3. `git commit -m <message>` 将当前寄存区的所有内容提交到本地库
4. `git status`查看仓库的状态 
   1. `Changes not staged for commit`未暂存以供提交的更改
   2. `no changes added to commit`没有添加要提交的更改
   3. `Changes to be committed`要提交的更改
5. `git diff <file>`查看被修改文件的变化

### 日志记录

1. `git log --pretty=oneline`显示从最近到最远的提交日志--如果版本回退，则该命令将只能看到回退版本及之前的提交日志
2. `git reflog`用来记录每一次命令
   1. `git reflog | head -n 10`查看前10条记录


### 版本回退

1. `git reset --hard head^/head^^/head~10/版本号`
   1. --soft 不会改变暂存区和工作目录
   2. --mixed 重置暂存区但不会改变工作目录
   3. --hard  会重置暂存区和工作目录

2. `git checkout commit_hash`切换版本,此时为游离的head(即head指向一个提交版本而不指向分支)

### 撤销修改

1. `git checkout --<file>` ||`git restore <file>` 将文件在工作区的修改全部撤销
   1. 如果该文件还没有被add到暂存区,此时会将文件撤销到与本地库最新版本相同的状态
   2. 如果该文件被add到了暂存区,则会撤销为添加到暂存区时的状态
2. `git reset head <file>` || `git restore --staged <file>`可以将文件从暂存区取回,重新放回到工作区
   1. head表示最新版本
3. 在工作区删除文件后同样发生了修改,与本地库不一致
   1. 可以在本地库中也删除该文件`git rm/add <file>`  `git commit`
   2. 误删了文件,从本地库中恢复文件`git checkout -- <file>`即用本地库的版本来替换工作区的版本

### 关联远程库

1. `git remove -v`查看关联的远程库地址以及别名--相同别名相同地址会有push和fetch两个(表示可以使用该别名推送和拉取)
2. `git remote add 别名 远程地址` 为远程库创建别名
3. `git remote rm 别名`
4. `git push 别名 分支` 向远程库push会pull时均以分支为单位
   1. push时若别名代表远程库的https协议的地址,则需要输入密码
   2. windows上的凭据管理器使用git连接github时会记录github的账号--故使用git只能在windows上登录一个github账号(或者在凭据管理器中手动删除对github账号的记录)
5. `git pull 别名 分支`
6. `git clone 远程地址` clone时无需登录github账号
   1. 拉取代码
   2. 初始化本地库(相当于执行了git init)
   3. 为远程地址创建别名
7. 在git中push时通过shh协议实现免密登录(需要在windows的home目录和github中配置shh密钥才能得到shh协议的地址)

### 分支管理

1. `git branch`查看分支
2. `git branch <name>`创建分支
3. `git checkout <name> || git switch <name>`切换分支
4. `git checkout -b <name> || git switch -c <name>`创建+切换分支
5. `git merge <name>` 合并到当前分支
6. `git branch -d <name>`删除分支
7. `git branch -D <name>`删除一个没有被合并过的分支(即强制删除)

#### 	BUG分支

1. `git stash`将当前工作目录隐藏(之后可以切换到其它分支，切回后可以恢复该分支的状态)
2. `git stash list`   `git stash pop`|| `git stash apply    git stash drop` 恢复分支状态同时删除stash内容
3. `git stash apply stash@{0}`恢复指定的stash
4. `git cherry-pick 版本号`合并一个特定的提交到当前分支

 ### 标签管理

> 标签相当于为某个提交版本的hash值起了一个别名

1. `git tag`   `git show <tagname>`查看标签
2. `git tag <name> [commit_hash]`为提交版本打标签(默认为head指向的版本打标签)
3. `git tag -d <tagname>`删除标签
4. `git push 别名 <tagname>`向远程库中推送标签
5. `git push origin --tags`可以推送全部未推送过的本地标签
6. `git push origin :refs/tags/<tagname>`可以删除一个远程标签

### idea中集成git和github





