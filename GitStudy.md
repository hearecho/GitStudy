# [Git&GitHub](https://git-scm.com/book/zh/v2)

> Git：分布式版本控制系统

### 1.简介

1. 协同修改：多人并行不悖的修改服务器的同一个文件
2. 数据备份：保存目录和文件的当前装填，还能保存每一个提交过的文件的历史状态
3. 版本管理：再保存每一个版本文件信息的时候要做到不保存重复数据，以节约存储空间，提高运行效率。这方面SVN采用的是增量式管理（只保存修改的部分），Git采取了文件系统快照的方式。
4. 权限控制：对团队参与的开发人员进行权限控制，对团队外贡献的代码进行审核。
5. 历史纪录：查看修改人，修改时间，修改内容，日志信息。将本地文件恢复到某一个历史状态。
6. 分支管理：允许团队在工作过程中多条生生产线同时推进任务，进一步提高效率。

### 2.安装-Windows

> [Git官网](https://git-scm.com/download/win)下载对应的版本，然后进行安装，可以安装到任意文件夹。
>
> 具体细节可以百度。

### 3.结构（本地）

![](img/结构.png)

### 4.代码托管中心

1. 在局域网下：
   - 可以搭建GitLab服务器，在外网也可以搭建
2. 在外网下：
   - GitHub 代码托管中心，国外
   - 码云 国内

### 5.本地和代码托管中心交互

1. 团队内部，本地于代码托管中心交互

![](img/本地和代码托管中心交互(团队内部).jpg)

2. 团队外部，本地与代码托管中心交互

![](img/本地和代码托管中心交互(外部).png)

### 6.Git命令行操作

#### 6.1本地库初始化

> 命令：git init
>
> 效果：
>
> ![](img/git.png)
>
> 注意：.git目录是隐藏文件夹，存放的是本地库相关的子目录和文件，不要删除，也不要没事去修改

#### 6.2设置签名

> 形式：
>
> ​	用户名：echo
>
> ​	Email地址：example@qq.com
>
> 作用：区分不同开发人员的身份
>
> 辨析：这里设置的签名和登陆远程库的账号，密码没有任何关系。
>
> 命令：
>
>  	1. 项目级别/仓库级别：仅在当前项目文件/仓库中起效
>      - git config user.name echo
>      - git config user.email example@example.com
>      - 信息保存位置  .git/config
> 		2. 系统用户级别：登陆当前操作系统的用户
>      - git config --global user.name echo
>      - git config --global user.email example@example.com
>      - 信息保存位置 ~/gitconfig
> 		3. 就近原则，项目级别优先。不能都不存在。

#### 6.3本地库操作命令：

##### 6.3.1 git status

~~~shell
git status   
#结果（文件是初始创建的文件，修改的文件显示结果会有不同）：
On branch master 
#第一行说明  此时实在 master 分支 
No commits yet
#第二行说明 此时并没有任何提交，也就是说本地库没有任何提交
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        GitStudy.md
        img/
#上面的内容说明 工作区 有 新的两个文件/文件夹 未跟踪的文件
#括号内容是提示，说明下一步应该 跟踪这些文件，将文件添加至暂存区
nothing added to commit but untracked files present (use "git add" to track)
#最后一行说明 没有文件被添加到暂存区，但是存在未跟踪的文件
~~~

![](img/gitstatus.png)

##### 6.3.2 git add  文件/文件夹



~~~shell
git add img/ GitStudy.md
#结果（文件是初始创建的文件，修改的文件显示结果会有不同）：
warning: LF will be replaced by CRLF in GitStudy.md.
The file will have its original line endings in your working directory.
#此警告没有影响，只是文末Linux和Windows形式不同，需要替换。这在安装的时候有选择
#使用 git status 查看此时 git的状态
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
		#现在 通过 git add 这些文件已经放在了暂存区里面
		#括号内容 是通过 rm 把刚才添加到暂存区的内容移除
        new file:   GitStudy.md
        new file:   img/git.PNG
        new file:   img/gitstatus.PNG
	    new file: ...
~~~

![](img/gitadd.png)

##### 6.3.3 git rm --cached \<file>

~~~shell
git rm --cached GitStudy.md
#结果
rm 'GitStudy.md'
#已经从暂存区移除 "GitStudy.d"
#git status 查看当前状态
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   img/git.PNG
        new file:   img/gitstatus.PNG
        new file:   ...
        #少了 GitStudy.md
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        GitStudy.md
        img/gitadd.PNG
        #多了 GitStudy.md
~~~

![](img/gitrm.png)

##### 6.3.4 git commmit \<file> -m "message"

~~~python
git commit GitStudy.md img/ -m "Git命令行操作"
#-m 后面添加 此次提交的信息  不加这个 -m  会进入一个 vim操作窗口 
#结果（文件是初始创建的文件，修改的文件显示结果会有不同）：
warning: LF will be replaced by CRLF in GitStudy.md.
The file will have its original line endings in your working directory.
[master (root-commit) 9bedc0a] Git命令行操作
 9 files changed, 98 insertions(+)
 create mode 100644 GitStudy.md
 create mode 100644 img/git.PNG
 create mode 100644 img/gitadd.PNG
 create mode 100644 img/gitrm.PNG
 create mode 100644 img/gitstatus.PNG
 create mode 100644 ...
#warning  是和一样的内容 可以忽略    
#master (root-commit)  master代表是主干 root-commit 表示是第一次提交 后面的提交就不会有了
#9bedc0a  此次提交的 id 标志
#Git命令行操作 -m 后面添加的此次提交的解释信息
#我们提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。 此时，可以运行带有 --amend 选项的提交命令尝试重新提交：git commit --amend
~~~

![](img/gitcommit.png)

##### 6.3.5 尝试修改文件文件后，执行上述的命令

1. 修改文件后执行  git status

   ~~~shell
   #结果  综合来说 就是修改的文件已经被追踪了，新添加的文件未被跟踪
   On branch master
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git checkout -- <file>..." to discard changes in working directory)
   
           modified:   GitStudy.md
   
   Untracked files:
     (use "git add <file>..." to include in what will be committed)
   
           img/gitstatus_change.PNG
   
   no changes added to commit (use "git add" and/or "git commit -a")
   #由于 修改过的文件夹 是已经被跟踪的文件 所以不会有 No commits yet
   #git add 这次命令是更新操作 而不是 添加操作
   #最后一行表示  可以直接 使用 commit 。或者还是按照原来的使用 git add  和 git commit
   ~~~

   ![](img/gitstatusChange.png)

2. 执行  git add  之后执行 git status 查看仓库状态

   ~~~shell
   #结果
   On branch master
   Changes to be committed:
     (use "git reset HEAD <file>..." to unstage)
   
           modified:   GitStudy.md
           new file:   img/gitstatusChange.PNG
   #两个文件明显的前缀对比，修改文件 是nodfied 新增文件就是 new file
   #括号里面的内容 就是用于回调版本 用到的命令
   ~~~

   ![](img/gitaddChange.png)

3. 执行git commit 之后，执行git status 查看仓库状态

   ~~~shell
   #结果
   #执行git commit 之后
   warning: LF will be replaced by CRLF in GitStudy.md.
   The file will have its original line endings in your working directory.
   [master 5d12dd3] Test Change cmmond
    2 files changed, 142 insertions(+), 55 deletions(-)
    create mode 100644 img/gitstatusChange.PNG
   #执行git status 查看仓库状态
   On branch master
   nothing to commit, working tree clean
   #新建的文件 会 create mode 100644 和前面的一样
   #修改的文件 不会create  因为已经创建
   ~~~

   ![](img/gitcommitChange.png)


##### 6.3.6 版本穿梭指令

1. git log 查看提交记录  commit记录

   ~~~shell
   #参数
   1. --pretty = oneline or --oneline 
   #每一天记录显示一行
   a988b78 (HEAD -> master) new Image
   6e99183 new Image
   5d12dd3 Test Change cmmond
   f96580b 新增图片
   9bedc0a Git命令行操作
   2. git relfog 
   #显示HEAD指针移动几步到其他版本
   a988b78 (HEAD -> master) HEAD@{0}: commit: new Image
   6e99183 HEAD@{1}: commit: new Image
   5d12dd3 HEAD@{2}: commit: Test Change cmmond
   f96580b HEAD@{3}: commit: 新增图片
   9bedc0a HEAD@{4}: commit (initial): Git命令行操作
   #一般结果
   commit 6e991837aec21bdf4e5fe93a719f393972009b87 (HEAD -> master)
   Author: echo <1540302560@qq.com>
   Date:   Mon Aug 6 16:00:56 2018 +0800
   
       new Image
   
   commit 5d12dd33dfb009ada5eaee38e00669a61e8aa667
   Author: echo <1540302560@qq.com>
   Date:   Mon Aug 6 15:53:42 2018 +0800
   
       Test Change cmmond
   
   .....
   #格式
   #commit  + 此次提交的Hash值(是一个这一次提交索引) + (HEAD->master)  HEAD 是一个指针 移动HEAD来改变指向版本
   #Author  + 签名
   #Date + 提交日期
   #提交时期添加的注释
   ~~~

   ![](img/gitlog.png)

2. 版本前进后退（不做演示）

   ~~~shell
   #最好先使用 git reflog 显示索引值
   #使用git reset --hard + 局部索引值命令 不用关心是前进还是后退，只需要知道你要转到的当时的那个版本的 索引值就可以了
   git reset --hard + 局部索引值(6e99183)不用全部
   #使用^符号  只能后退不能前进 一个^后退一个版本
   git reset --hard HEAD^^^ #后退三个版本，
   git reset --hard HEAD~3  #后退三个版本，只能后退
   #参数
   --soft #仅仅在本地库修改指针
   --mixed #在本地库修改指针，重置暂存区
   --hard #在本地库修改指针，重置暂存区和工作区
   ~~~

3. 文件永久删除后找回

   ~~~shell
   #就是通过版本回溯，--hard模式，使删除的文件回来
   #删除前 文件的状态就是必须提交到本地库
   #新增一个文件 文件的状态就是必须提交到本地库
   6098d38 (HEAD -> master) HEAD@{0}: commit: 测试文件
   1803d22 HEAD@{1}: commit: Change md
   a988b78 HEAD@{2}: commit: new Image
   6e99183 HEAD@{3}: commit: new Image
   .....
   #删除文件 
   4d2111d (HEAD -> master) HEAD@{0}: commit: delete test.txt
   6098d38 HEAD@{1}: commit: 测试文件
   1803d22 HEAD@{2}: commit: Change md
   a988b78 HEAD@{3}: commit: new Image
   6e99183 HEAD@{4}: commit: new Image
   ......
   #然后使用  git  reset --hard 6098d38 回到未删除的版本，进行修改后
   05cb462 (HEAD -> master) HEAD@{0}: commit: 修改测试文件
   6098d38 HEAD@{1}: reset: moving to 6098d38
   4d2111d HEAD@{2}: commit: delete test.txt
   6098d38 HEAD@{3}: commit: 测试文件
   ~~~

##### 6.3.7 文件比较操作 git diff \<文件名> 不加文件名比较多个文件

1. 和暂存区进行比较 （默认）

   ~~~shell
   git diff GitStudy.md
   #红色删除 绿色新增
   ~~~

   ![](img/gitdiff1.png)

2. 和本地库进行比较

   ~~~shell
   git diff [本地库历史版本] <file>
   ~~~



#### 6.4 [Git分支](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%AE%80%E4%BB%8B)

##### 6.4.1 介绍

> 在版本控制过程中，使用多条线推进多个任务，提高开发效率
>
> 1. 创建分支，使其它任务在其他分支进行推进。
> 2. 当分支任务经过多次迭代完成之后，合并到主干分支，然后可以选择删除该分支。
> 3. 合并过程可能会出现同一个文件被多个分支在同一个地方进行了修改，而且不相同，所以应该使这些文件相同之后合并分支。
> 4. 热修复 hot_fix 使线上应用不停止修复一些bug

![](img/分支.png)



##### 6.4.2 命令

1. 创建分支。 git branch (分支名字)

2. 查看当前的所有分支。git branch -v

   ~~~shell
    hot_fix be4a622  new Image
   * master  be4a622  new Image
   # * 表示当前所在的分支 绿颜色
   #后面参数表明： 此时两个分支在同一个进度
   ~~~

![](img/gitbranch-v.png)

3. 切换分支。 git checkout (分支名)

   ~~~shell
   #切换到 hot_fix 分支
   Switched to branch 'hot_fix'
   #在 hot_fix 分支提交新的进度，此时查看分支状态就会发现此时的进度已经不一样了
   * hot_fix 4def57d Change on branch hot_fix
     master  be4a622  new Image
   ~~~

   ![](img/gitcheckout.png)

   ![](img/gitcheckout1.png)

4. 合并分支。 git merge (分支名)

   ~~~shell
   #执行合并分支命令前，先把分支切换到主分支上，然后在执行合并分支的命令
   Updating be4a622..4def57d
   Fast-forward
    GitStudy.md         |  40 +++++++++++++++++++++++++++++++++++++++-
    img/gitbranch-v.PNG | Bin 0 -> 7462 bytes
    2 files changed, 39 insertions(+), 1 deletion(-)
    create mode 100644 img/gitbranch-v.PNG
   #查看分支状态
    hot_fix 4def57d Change on branch hot_fix
   * master  4def57d Change on branch hot_fix
   ~~~

   ![](img/gitmerge.png)

5. 删除分支 git branch -d (分支名)

   ~~~shell
   $ git branch -d hot_fix
   Deleted branch hot_fix (was 4def57d).
   ~~~

6. 冲突解决

   1. 合并时如果有冲突会进入特殊状态，此时冲突文件里面会产生一些特殊符号
   2. 解决冲突，就是先删除特殊符号，特殊符号是为了确认位置。
   3. 编辑文件到自己满意的程度
   4. git add 文件名
   5. git commit -m 信息 注意：不能加文件名

### 7.和github交互

#### 7.1命令交互

##### 7.1.1 创建本地远程库别名

~~~shell
#查看远程库别名
git remote -v
#创建远程库别名
git remote add + 别名 +仓库地址
git remote add origin https://github.com/hearecho/GitStudy.git
#orgin  就是别名
$ git remote -v
origin  https://github.com/hearecho/GitStudy.git (fetch)
origin  https://github.com/hearecho/GitStudy.git (push)
#push 推送 fetch 拉取
~~~

##### 7.1.2推送

~~~shell
git push orgin master
~~~

##### 7.1.3克隆

~~~shell
git clone + 远程仓库地址
#克隆下来之后 是一个文件夹，文件夹内部也是一个项目环境
#同时可以进行上传，下载（都是自己的情况下）
~~~



