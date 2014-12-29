title: Git学习之使用Github
date: 2014-12-26 20:48:50
categories: Git
tags:
---
安装了Git之后我们要使用Github怎么办呢？下面就简单的介绍一下安装完Git之后怎么配置吧。

在全局配置了Git

`$ git config --global user.name "Your Name"`
`$ git config --global user.email "email@example.com"`
<!-- more -->
##接下来我们来生成ssh

之前有过简单的介绍(当时实在Mac下配置的)：<http://dowhile.net/2014/11/30/onehexo/>

在win下有一点点的小不同，所以在这里提一下。先执行下边的命令：

`ssh-keygen -C "email@example.com" -t rsa`

接着回车，然后中间会让你输入一个密码。下边有个图仅供参考：

![](http://yangxiaolei.qiniudn.com/3.PNG)

从画红色线条的目录下可以看到生成的ssh

我们把**id_rsa.pub**用文本打开，内容复制下来。接下来登录的你的Github帐号。

如下图点击右上角的设置，再点击左边的SSH。再点击ADD  SSH key
把刚才复制的内容粘贴进来保存就好了。

![](http://yangxiaolei.qiniudn.com/ssh.PNG)

接下来执行

`ssh -T git@github.com`

来检测是否连接成功！

如果成功就会提示Hi UersName.....
---


##添加远程库

现在的情景是，你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举多得。

首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：

![](http://yangxiaolei.qiniudn.com/github1.png)

在Repository name填入`learngit`，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：

![](http://yangxiaolei.qiniudn.com/github2.png)

目前，在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令：

`$ git remote add origin git@github.com:yangxiaoleigithub/learngit.git`

请千万注意，把上面的yangxiaoleigithub替换成你自己的GitHub账户名，否则，你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。

添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

下一步，就可以把本地库的所有内容推送到远程库上：
```
$ git push -u origin master
Counting objects: 19, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (19/19), done.
Writing objects: 100% (19/19), 13.73 KiB, done.
Total 23 (delta 6), reused 0 (delta 0)
To git@github.com:yangxiaoleigithub/learngit.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。

由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样：

![](http://yangxiaolei.qiniudn.com/github3.png)

从现在起，只要本地作了提交，就可以通过命令：

`$ git push origin master`

###SSH警告

当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入`yes`回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

`Warning: Permanently added 'github.com' (RSA) to the list of known hosts.`

这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入yes前可以对照[GitHub的RSA Key的指纹信息](https://help.github.com/articles/what-are-github-s-ssh-key-fingerprints/)是否与SSH连接给出的一致。

##从远程库克隆

现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

首先，登陆GitHub，创建一个新的仓库，名字叫`gitskills`：

![](http://yangxiaolei.qiniudn.com/github4.png)

我们勾选`Initialize this repository with a README`，这样GitHub会自动为我们创建一个`README.md`文件。创建完毕后，可以看到`README.md`文件：

![](http://yangxiaolei.qiniudn.com/github5.png)

现在，远程库已经准备好了，下一步是用命令git clone克隆一个本地库：

```
$ git clone git@github.com:yangxiaoleigithub/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done.

$ cd gitskills
$ ls
README.md
```

注意把Git库的地址换成你自己的，然后进入`gitskills`目录看看，已经有`README.md`文件了。








