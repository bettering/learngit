Git is a version control system.
Git is free software.
1 创建版本库
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
选择位置，做一个空目录


2 把这个空目录变为GIT的仓库
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/


3  git add  把文件添加到仓库   把文件添加到暂存区
$ git add readme.txt

4  git commit 把文件提交到仓库   把暂存区里面的文件添加到分支
$ git commit -m "wrote a readme file"（-m 后面是解释日志所做的事情）

5 git status 监听仓库动态

6 git diff+<文件名> 查看修改了什么内容

7 git log --pretty oneline 查看日记，看到提交的内容
$ git log --pretty=oneline
3628164fb26d48395383f8f31179f24e0882e1e0 append GPL
ea34578d5496d7dd233c827ed32a8cd576c5ee85 add distributed
cb926e7ea50ad11b8f9e909c05226233bf755030 wrote a readme file（前面是GIT，id）


8 回退到上一版本
$ git reset --hard HEAD^
   --hard 后面接版本ID 想回到哪个就写那个ID版本号 相当于指针
   
9 git reflog 记录每一次命令
可以查看命令ID

10  $ cat <readme.txt> 查看当前文件内容

11 工作区---是在电脑里面建立的空目录
   版本库---是.git隐藏的文件目录
        版本库里面有暂存区stage   和    Git自动创建第一个分支master
        
12  用git diff HEAD -- <readme.txt>命令可以查看工作区和版本库里面最新版本的区别：
*   第一次修改 -> git add -> 第二次修改 -> git add -> git commit

13   git checkout -- <file>可以丢弃工作区的修改：    file是文件名

14  $ git rm test.txt  删除文件从版本库中


15 $ git remote add origin git@github.com:michaelliao/learngit.git关联本地仓库到远程库
   $ git push -u origin master   把本地库所有内容提交到远程库
   
   以后只要本地作了提交，就可以通过命令：
    $ git push origin master 就可以把master上所有东西推送到Github远程库
    
16 远程库准备好的情况下 
  $ git clone git@github.com:bettering/file.git 克隆一个本地库
  $ cd file
  $ ls
  README.md
  
17  创建于合并分支
 首先，我们创建dev分支，然后切换到dev分支：
 $ git checkout -b dev
 gitcheckout和 -b参数表示创建和切换
 相当于下面两条命令
 $ git branch dev
 $ git checkout dev
 然后，用git branch命令查看当前分支：
 $ git branch
* dev     *表示当前分支
  master
  
  切换回主分支master
  $ git checkout master
  
  把dev的成果合并到master上的命令是：
  $ git merge dev
  git merge命令用于合并指定分支到当前分支。
  然后删除dev分支
  $ git branch -d dev
  
  （查看分支：git branch
  创建分支：git branch <name>
  切换分支：git checkout <name>
  创建+切换分支：git checkout -b <name>
  合并某分支到当前分支：git merge <name>
  删除分支：git branch -d <name>）
  
18  当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
    用git log --graph命令可以看到分支合并图。
    
19 禁用fast  forward模式，可以看到历史改动，可以看到dev分支
    只用dev，看不到历史改动
    $ git merge --no-ff -m "merge with no-ff" dev
    -m 把commit描述写进去

20修复BUG，用分支，修复后合并分支，删掉BUG分支

21 $ git stash把当前工作现场隐藏起来
   当工作现场隐藏起来的时候可以用$ git stash list查看
   工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
   一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
   另一种方式是用git stash pop，恢复的同时把stash内容也删了：
   
22 开发新功能feature，最好再建立一个分支
   如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。


23 git remote -v显示远程库更详细的信息
 
   多人协助
  
  / 推送分支：git push origin master 推送本地分支上所有代码
             git push origin dev    只推送dev分支到远程库
1，该分支   指的是【$ git push origin 本地分支名】 这句话中的分支
 2，origin只是被clone的Github上的版本库，相当于当前被clone的版本库gitskills的别名就是 origin
 3，$ git push origin master 这句话中的master是指本地的master，并非是github中远程库的master。
 / 抓取分支
 $ git clone git@github.com:bettering/learngit.git   bettering是github帐户名    learngit.git是ropo名字
 要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是用这个命令创建本地dev分支：
   $ git checkout -b dev origin/dev
   修改后推送到远程库

  4，要是在本地版本库中创建分支 ceshi  与github中远程库origin的 一个分支 ceshi_1相关联（假设远程库中已经有ceshi_1分支）【$ git checkout -b ceshi origin/ceshi_1】，那么要是在 本地执行

  $ git push origin ceshi ——意思是在github上的远程库（origin）上创建分支 ceshi，并将本地ceshi分支的内容推送（push）到远程库（origin）上的新分支 ceshi上，而不是 推送到所谓与之关联的 ceshi_1上
因此要是想推送到相关联的ceshi_1上，就要这样写 $ git push remote ceshi:ceshi_1
所以在创建本地版本库的分支和远程分支相关联的时候，名称最好起的一样
 
 恰巧你推送的分支与队员分支有冲突
 建立本地分支与远程origin/dev建立连接
 $ git branch --set-upstream dev origin/dev
 再把origin/dev抓取下来
 在本地合并，解决冲突，再推送到远程
 
 总结：多人协作的工作模式通常是这样：
首先，可以试图用git push origin branch-name推送自己的修改；
如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
如果合并有冲突，则解决冲突，并在本地提交；
没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！
如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。
  
  
  在Git中打标签非常简单，首先，切换到需要打标签的分支上：
$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'
然后，敲命令git tag <name>就可以打一个新标签：
$ git tag v1.0
可以用命令git tag查看所有标签：
$ git tag
v1.0
默认标签是打在最新提交的commit上的。




创建标签
首先切换到要创建标签的分支上
$ git branch
敲命令git tag <name>就可以打一个新标签：
$ git tag v1.0
git tag可以查看所有标签
  
  
  


