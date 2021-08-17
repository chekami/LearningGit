git 分布式版本控制系统
所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等

1.打开git bash
2.创建版本库（相当于工作目录） mkdir FirstRepository  //当需要直接进入已有的某个目录时候，这个就是非必须操作
3.切入某个版本库 cd FirstRepository
4.查看当前目录 pwd  //任何时候都可以执行该命令，查看工作当前目录
5.版本库初始化 git init  //新创建的版本库，第一次切入后，需要对版本库进行初始化，初始化完成后，改工作目录就会变成主分支（master),并且目录下会自动创建一个隐藏文件夹.git，是Git的版本库，Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
6.查看当前目录下的所有文件 ls -ah
7.将文件添加到当前仓库需要两步  1.git add readme.md  //用命令git add告诉Git，把文件添加到仓库的暂存区
                           2.git commit -m "wrote a readme file"  //用命令git commit告诉Git，把文件由暂存区提交到当前分支，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。因为commit可以一次提交很多文件，所以你可以多次add不同的文件

8.查看仓库当前状态  git status  //可以知道哪些文件被修改过
9.具体查看文件修改了什么内容  git diff readme.md  //看完之后，用ctrl+d退出查看模式
测试版本回退
	版本1
	版本2
10.回到历史版本  git reset --hard commit_id   // commit_id为HEAD^表示返回上一个版本，为HEAD^^表示返回上上一个版本，几个^符号表示往上多少个版本，简便写法HEAD~n表示返回往上第n个版本；从历史版本跳入未来版本，比如从版本1跳入版本2，需要版本2的commit id，一般输入前几位即可
11.查看版本库当前状态  git log  //如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数
12.查看所有提交记录  git reflog
13.工作区（当前文件夹目录） 利用add将文件提交到版本库  版本库：暂存区（stage）、分支（master） //第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
14.git管理的是修改，而非文件  例如：第一次修改 -> git add -> 第二次修改 -> git commit  //第二次修改未提交
									第一次修改 -> git add -> 第二次修改 -> git add -> git commit  //此时第二次修改后的提交
15.查看工作区和版本库里面最新版本的区别  git diff HEAD -- readme.txt
16.撤销修改  第一类：工作区的修改，还未提交到暂存区 git checkout -- readme.md
			 第二类：工作区的修改，已经提交到暂存区 git reset HEAD readme.md  //此时回到了第一类，接着按照第一类做法
			 第三类：已经提交了不合适的修改到版本库 git reset --hard commit_id
17.删除文件 rm TestDelete.txt
18.提交删除操作 git rm TestDelete.txt
				git commit -m "remove TestDelete.txt"
19.把误删的文件恢复到最新版本 git checkout -- TestDelete.txt  //git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”，注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！ 这种方式针对没有提交过的删除操作，针对已经提交过的删除操作，需要使用版本回退功能
20.远程仓库设置操作
	第1步：创建SSH Key  $ ssh-keygen -t rsa -C "youremail@example.com"
	第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：
21.添加远程仓库
	首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库
	把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库
		$ git remote add origin git@github.com:michaelliao/learngit.git  //请千万注意，把上面的michaelliao替换成你自己的GitHub账户名，远程库的名字就是origin，这是Git默认的叫法
		$ git push -u origin master  //把本地库的所有内容推送到远程库上，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来
22.从远程库克隆  $ git clone git@github.com:michaelliao/gitskills.git
23.创建与合并分支
	创建分支：git branch <name>
	查看分支：git branch
	切换分支：git checkout <name>或者git switch <name>  //switch方式只能在最新版的git中使用
	创建+切换分支：git checkout -b <name>或者git switch -c <name>
	合并某分支到当前分支：git merge <name>
	删除分支：git branch -d <name>
	看到分支合并图：git log --graph

24.分支变基
	将分支的基变到master最新的提交上，避免分支线过于复杂
	1、切换到要提交的分支
	$ git checkout mywork
    2、变基并提交
	$ git rebase origin
	2、等价操作
	$ git checkout mywork
	$ git rebase origin
	





									