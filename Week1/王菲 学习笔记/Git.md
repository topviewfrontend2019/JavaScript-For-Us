1. 创建版本库
 
  -  mkdir 文件名
  -  cd    文件名
  -  pwd
  -  ls
  -  git init
  -  git add <file>
  -  git commit -m <message>

+ 时光机
  + git status ->用于查看工作区当前状态
  + git diff   ->查看修改的内容
  + git log    ->最近三次提交，由上到下为最近到最早
  + git log --pretty=online
  + git reset --hard HEAD^  ->HEAD为当前版本，HEAD^为上一个，HEAD^^为上上个，HEAD~100往上一百个
  + git reflog -->查看被记录的命令从而找到未来的commit id
  + git reset --hard commit id
  + git checkout -- file ->丢弃**工作区**的修改，总之，就是让这个文件回到最近一次git commit或git add时的状态。
  + git reset HEAD file ->命令既可以回退版本，也可以把**暂存区**的修改回退到工作区。当我们用HEAD时，表示最新的版本。
  + git rm ->删除文件
+ 远程库
  + $ git remote add origin git@github.com:michaelliao/learngit.git
  + $ git push -u origin master ->之后git push origin master 就可
  + $ git clone git@github.com:michaelliao/gitskills.git

+ **分支管理**
  + git checkout -b dev
  + git branch
  + git checkout master
  + git merge dev ->合并指定分支到当前分支
  + git branch -d dev ->删除分支
  + git log --graph ->分支合并图
  + git merge --no-ff-m"" dev ->这样就不会丢失分支信息
  + git stash ->储存当前工作现场并清空
  + git stash list
  + git stash apply stash@{0}
  + git stash drop
  + git stash pop ->恢复的同时删除stash内容
  + git branch -D <name> ->丢弃一个没合并的分支
  + **多人协作**
     + git remote -v
     + git push origin master
     + git pull 
  + rebase
     + git rebase
+ 标签管理
  + git tag 
  + git tag <tagname>
  + git push origin <tagname>
  + git push origin --tags
  + git tag -d <tagname>
  + git push origin :refs/tags/<tagname>

