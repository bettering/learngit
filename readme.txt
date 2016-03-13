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
  
  
  
  
  


