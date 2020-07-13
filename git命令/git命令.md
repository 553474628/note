##### 常用操作

+ git log --author="$(git config --get user.name)" --pretty=tformat: --numstat | awk '{ add += $1 ; subs += $2 ; loc += $1 - $2 } END { printf "added lines: %s removed lines : %s total lines: %s\n",add,subs,loc }'     #git统计的提交代码的数量

+ git config --global user.name "name"   #配置用户信息（去掉后面的名字是查询信息）
+ git config --global user.email "email"
+ git pull     #拉取分支上的内容
+ git status     #修改的文件
+ git diff    #更改的具体内容（+ 代表新加，- 代表删除）
+ git blame <file>      #查看该文件的提交记录
+ git add <file>       #添加某一个文件
+ git add .     #添加所有文件
+ git commit -m "name"     #提交到本地代码库
+ git commit -s     #添加了Signed-off-by（ 有的项目中需要进行CI 校验）
+ git commit --amend     #修改最新一条提交信息的 log 内容
+ git push origin    #提交到远程分支
+ git checkout -- <file>    #当你在工作区修改想要丢弃时（撤销修改内容）
+ git reset HEAD <file> (不加HEAD，直接输入commitId可以保存当前修改)   #add到暂存区想要撤销修改时
+ git reset --hard HEAD~10    #commit到本地版本库以后想要回退
+ git branch -a     #查看当前有那些分支
+ git branch -vv    #可以查看所在的分支，比如stable或者dev
+ git branch <name> -t stable(远程分支名)    #-t是追踪远程分支
+ git checkout -b <name> -t stable(远程分支名)    #创建一个分支并切换到stable分支
+ git cherry-pick <commitId>    #切换到提交的id并保留你的修改

- git log <commitId>    #查看其中一条记录
- git log --graph    #可以看到分支合并图
- git merge 操作合并分支会让两个分支的每一次提交都按照提交时间（并不是push时间）排序，并且会将两个分支的最新一次commit点进行合并成一个新的commit，最终的分支树呈现非整条线性直线的形式
- git rebase 操作实际上是将当前执行rebase分支的所有基于原分支提交点之后的commit打散成一个一个的patch，并重新生成一个新的commit hash值，再次基于原分支目前最新的commit点上进行提交，并不根据两个分支上实际的每次提交的时间点排序，rebase完成后，切到基分支进行合并另一个分支时也不会生成一个新的commit点，可以保持整个分支树的完美线性

另外值得一提的是，当我们开发一个功能时，可能会在本地有无数次commit，而你实际上在你的master分支上只想显示每一个功能测试完成后的一次完整提交记录就好了，其他的提交记录并不想将来全部保留在你的master分支上，那么rebase将会是一个好的选择，他可以在rebase时将本地多次的commit合并成一个commit，还可以修改commit的描述等。



##### 遇到问题

```shell
git提交代码时出现错误：error : unpack failed : error Missing commit XXX，XXX代表提交的版本号。
原因：本地索引出错。
解决方法：
1. git gc
2. git pull --rebase（过程中遇到冲突需要先解决冲突，再git add .）
3. git push  （gerrit上直接repo upload .就行）
```

```shell
如果只想提交一部分文件就用stash
git add file01.txt
git stash    #隐藏其他修改，存入暂存区
git commit -s
git stash pop  #恢复的同时把stash内容也删了   
           #也可以用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除
           
#出现问题参考  https://www.jianshu.com/p/efb9f2f1bd05
```

