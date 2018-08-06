# Git&GitHub

> Git：分布式版本控制系统

###1.简介

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

1. 本地库初始化

   > 命令：git init
   >
   > 效果：
   >
   > ![](img/git.png)
   >
   > 注意：.git目录是隐藏文件夹，存放的是本地库相关的子目录和文件，不要删除，也不要没事去修改

2. 设置签名

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
   >  	2. 系统用户级别：登陆当前操作系统的用户
   >      - git config --global user.name echo
   >      - git config --global user.email example@example.com
   >      - 信息保存位置 ~/gitconfig
   >  	3. 就近原则，项目级别优先。不能都不存在。

3. 本地库操作命令：

   ~~~shell
   git status
   #结果：
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

   