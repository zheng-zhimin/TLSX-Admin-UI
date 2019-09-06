# Git 版本控制器

## 一、 Git 简介

> 什么是git？

Git是目前世界上最先进的分布式版本控制系统（没有之一）。

> Git的诞生

![](https://gss3.bdstatic.com/7Po3dSag_xI4khGkpoWK1HF6hhy/baike/w%3D268%3Bg%3D0/sign=c87aa59942a7d933bfa8e3759570b62e/5882b2b7d0a20cf4f664615276094b36adaf9943.jpg)

​	 Linus虽然创建了Linux，但Linux的壮大是靠全世界热心的志愿者参与的，这么多人在世界各地为Linux编写代码，那Linux的代码是如何管理的呢？

​	事实是，在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码！

​	到了2002年，Linux系统已经发展了十年了，代码库之大让Linus很难继续通过手工方式管理了，社区的弟兄们也对这种方式表达了强烈不满，于是Linus选择了一个商业的版本控制系统BitKeeper，BitKeeper的东家BitMover公司出于人道主义精神，授权Linux社区免费使用这个版本控制系统。

​	安定团结的大好局面在2005年就被打破了，原因是Linux社区牛人聚集，不免沾染了一些梁山好汉的江湖习气。开发Samba的Andrew试图破解BitKeeper的协议（这么干的其实也不只他一个），被BitMover公司发现了（监控工作做得不错！），于是BitMover公司怒了，要收回Linux社区的免费使用权。

Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！



## 二、Git的使用

##### 1. 创建版本库	

``git init``   

瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个`.git`的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

##### 2. 配置当前版本库的信息

```git config  --global user.name 'xxx'`	``

``git config  --global user.email 'xxx@qq.com'``

##### 3. 添加文件

``git add <file_name>``

``````
git add 1.html  添加1.html

git add .       .添加修改文件到仓库

git add -all    -all  添加所有文件

``````

​	

##### 4. 提交文件

``git commit ``

````
$ git commit -m '修改了冲突'
-m 提交的信息
````

![](./git/git.jpg)

###### 4.1 查看冲突

`git diff` 

##### 5 . 查看git状态

`` git status ``

##### 6. 版本控制

`` git reset ``	

> 版本操作

``````
跳到当前版本 git reset --hard HEAD  
跳到上一版本 git reset --hard HEAD^  
跳到上上版本 git reset --hard HEAD^^
跳到指定版本 git reset --hard commit_id
``````

> 看提交历史

``git log``   查看当前历史

`````
git log --pretty=oneline     只输出一行
`````

``git reflog``  查询所有提交历史

`````
git reflog 以便确定要回到未来的哪个版本
`````

##### 7. 撤销修改

``git checkout -- file_name``

``````
场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file_name。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file_name，就回到了场景1，第二步按场景1操作
``````

##### 8 . 删除文件

`````
2.git rm readme.txt
	git commit -m “delete readme.txt"	
    
撤销办法：
    找回删除文件（版本会退）：使用 git reset —hard HEAD^
`````

##### 9. 分支管理

	查看分支：git branch
	
	创建分支：git branch <name>
	
	切换分支：git checkout <name>
	
	创建+切换分支：git checkout -b <name>
	
	合并某分支到当前分支：git merge <name>
	
	删除分支：git branch -d <name>
##### 10. 远程仓库

> 关联远程仓库 **remote**

`git remote add origin https://github.com/lamp402213226/php110.git`

> 推送代码到仓库 **push**

`git push -u origin master`	将代码推送到master分支上

`git push -u origin master:master`		将本地的master分支上的代码推送到服务器上的master分支上

````
git push -u origin master:master -f 
-f 强制推送  一般不要使用
````

> 拉取 **pull**

`git pull origin master` 	拉取服务器上的版本

> 获分支新的的版本 **fetch**

` git fetch`

> 克隆版本库 **clone**

`git clone https://github.com/lamp402213226/test.git`

## 三、团队协作

#### 场景应用

###### 1.  组长

````
1. 在项目中初始化仓库	git init
2. 配置git的用户名 和 邮箱	git config ..
 	  			注意配置自己的邮箱 权限问题	
  	 		*** 将自己的组员 添加到项目的协作者
3. 添加并且提交到本地的版本库	git commit	
4. 添加本地的和远程仓库的关联	git remote
5.推送	
   git push -u origin master:master 
   		-u 声明提交的用户  一般第一次提交的时候使用
````

###### 2. 组员

```
1. 进行克隆
2. 配置版本库的用户名和邮箱

git config  --global user.name 'zheng-zhimin'
git config  --global user.email '1453175095@qq.com'
3. 添加新的分支
git checkout -b zzm
推送  git push origin zzm:zzm
```

###### 3. 合并分支

```
1. 查看当前的分支 git fetch
2. 合并 git merge origin/xxxx 	
			注意：合并要查看当前的工作区和版本库是否一致  git status
```



##比远程仓库版本低处理方法
```

在团队开发中，git的使用已经很常见了，博主也是经常使用coding，github等代码托管平台。在多人协同开发中，我们经常会遇到这样的问题：A在本地开发完成后，将代码推送到远程，这时候B的本地代码的版本就低于远程代码的版本，这时候B该如何从远程拉取最新的代码，并与自己的本地代码合并呢？ 具体步骤如下：

查看远程仓库:
git remote -v
复制代码
比如 在步骤一中，我们查看到远程有一个叫origin的仓库，我们可以使用如下命令从origin远程仓库获取最新版本的代码
git fetch origin master:temp
复制代码
上面代码的意思是：从远程的origin仓库的master分支下载到本地master并新建一个temp分支

查看temp分支与本地原有分支的不同
git diff temp
复制代码
将temp分支和本地的master分支合并
git merge temp
复制代码
现在，B的本地代码已经和远程仓库处于同一个版本了，于是B可以开心coding了。

最后再提一下，上面的步骤中我们创建了temp分支，如果想要删除temp分支，也是可以的，命令如下：

git branch -d temp
```
##在推的时候遇到黄色提示
```
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/zheng-zhimin/web1.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
混帐拉就OK了再执行推操作！


