#  工作中总结的常用git命令以及使用场景

### git init

用于初始化git仓库

用法：cd到项目根目录使用，该项目就会被git管理，根目录生成.git文件

### git init your_project

该命令直接创建项目文件夹，并纳入git管理，项目根目录生成.git

.git文件解析：

- HEAD文件用于存放指向当前分支的指针，编辑该文件，等同与checkout命令切换分支，HEAD存储的是一次commit
- config文件用于存放本地仓库配置信息（例如用户名和密码）
- refs/heads目录下存放所有分支，例如heads下的master文件，内容就是commit的hashcode，可用cat master查看该hashcode
- objects用于存放git对象,git主要commit，tree，blob三种对象，其中commit存放一次提交的快照，其中包含若干tree和blob对象。tree相当于文件夹，每一个tree里面可有又包含tree和blob。而blob对象则用来存放文件



------

### git cat-file -t your_code

用于查看git对象类型，查看your_code的类型

可选参数

- -p 查看对象内容
- -t 查看对象类型

***

### git config --global user.name 'your_name'

### git config --global user.email 'your_email'

用于设置git用户名和密码

可选参数：

- --global 当前用户对所有仓库有效

- --local 只对当前git仓库有效，因此在其他仓库无法使用该参数命令，如果当前仓库同时设置有global和local的用户名和邮箱，local的优先级更高

***

### git config --list --global

用来查看当前git配置（一般用于查看git用户和邮箱）

***

### git add your_file

将your_file添加到暂存区

***

### git mv your_file your_new_file

修改文件名

***

### git log -n2 --oneline

查看日志信息

可选参数：

- -n2 查看最近两条提交记录，如果是-n3就是最近三条记录
- --oneline 以简洁的方式查看git提交记录
- --all查看所有分支的历史提交记录
- --graph使git提交历史图形化，更易于浏览

***

### git branch -v

查看本地的分支

***

### gitk

打开图形化工具

***

### git checkout your_branch

切换到your_branch分支，该命令需要在根目录下使用

### git checkout your_commit

如果your_commit为某次commit的hashcode，这中状态叫做分离头指针，此时HEAD将不会指向任何分支，而是基于这次commit进行工作，此命令需慎用。例如：假如使用该命令后，对工作目录有了新的变更，进行commit后，此时再切换其他分支会导致这次commit丢失，因为git只会保留基于分支的变更。

### git branch your_branch commit

该命令基于commit创建新分支（your_branch），用于解决以上导致变更丢失问题

### git checkout -b your_branch2 your_branch1

基于your_branch1创建your_branch2,并切换到新分支，-b作用是切换到新建分支

### git checkout -- your_file

使工作区文件和暂存取保持一致，工作区文件变更将会丢失

***

### git diff your_commit1 your_commit2

比较两次提交的异同

### git diff --cached

比较暂存区和HEAD的差异

### git diff

比较工作区和暂存区的差异

***

### git branch -D your_branch

删除your_branch分支

***

### git commit --amend

修改最近一次的commit的注释内容

***

### git reset HEAD

使暂存区和HEAD内容一致（所有文件）

### git reset HEAD -- your_file1 your_file2

使暂存取部分文件（your_file1和your_file2）恢复为和HEAD一致

### git reset --hard your_commit

将头指针指向your_commit，后面的所有commit将会丢失，暂存取和工作区的内容，都恢复为your_commit

***

### git rm your_file

如果当前commit不想再要your_file文件，使用该命令，删除状态先保存到暂存取，再次commit就会删除该文件

***

### git remote add your_alias your_repository_path

添加远程git仓库，your_alias为别名，your_repository为远程仓库地址

### 