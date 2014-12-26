title: 在Gitcafe上建立你自己的博客（一）
date: 2014-11-30 10:25:57
categories: Git
tags: Hexo
---
刚开始用GitHub不久，就了解到可以通过GitHub Pages来创建属于自己的静态博客。GitHub官方推荐使用的是Jekyll，但是由于我不太熟悉Ruby折腾了几天之后感觉太麻烦，也就放下了。直到多看了一眼[Hexo](http://hexo.io/)，这个逼格极高的程序猿写作方式。但是在国内Git访问太慢严重影响到了心情，后来发现gitcafe是天朝本地化的github，接下来给大家来介绍怎么通过Hexo优雅的写博客。我是在Mac下搭建的，中间过程中可能有些回和其他系统有些不同。
<!-- more -->

##我把它分为四大步骤
###一、 

#### 环境的搭建

###二、

####主题的设计

###三、

####博客发表

###四、

####后续细节的处理
***
##1.Hexo 介绍
***
+ Hexo 是一个简单地、轻量地、基于Node的一个静态博客框架。通过Hexo我们可以快速创建自己的博客，仅需要几条命令就可以完成。

+ 发布时，Hexo可以部署在自己的Node服务器上面，也可以部署github上面。对于个人用户来说，部署在github上好处颇多，不仅可以省去服务器的成本，还可以减少各种系统运维的麻烦事(系统管理、备份、网络)。所以，基于github的个人站点，正在开始流行起来…
Hexo的官方网站<http://hexo.io/>,也是基于GitHub构建的网站。

+ 静态博客编译之后是纯html页面,优点就是支持它的环境十分好找,例如github、gitcafe、七牛云存储等站点都支持静态页面托管,自然是我们的首选了。由于github page在国内访问较慢,我用gitcafe做示范。gitcafe是天朝本地化的github,同样提供展示页和域名绑定功能,不需要备案,就是爽。

+ 但是静态博客并非没有缺点。动态博客更新文章时,脚本是不变的,只需要更新数据库。静态博客要频繁改动文件,不支持增量式上传的东西,比如ftp,就难于管理。此外,还要十分熟悉git各种命令,才能部署页面。


***

##2.环境的搭建


***
+ ###安装Git
Git的安装教程网上有太多太多了，我就不在这里多说什么了。给个链接，这里有很详细的关于[Git的教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000).顺便给上下载地址：<http://git-scm.com/download/>
后边会详介绍 SSH密钥的创建
***
+ ###安装Node
	到[Node.js](http://nodejs.org/)官方网站下载你对应的平台的最新版本，一键安装即可。(现在的版本好像内置就带有npm包管理)
	
	Liux下：
	
	`$ sudo apt-get install nodejs `
	
	`$ sudo apt-get install npm`
	
	*windows或者mac下,直接到node.js官网下载安装。windows还要设置环境变量,把node.js安装路径写进path里面,用半角分号分隔。*
	***
+ ###markdown编译器


	windows下推荐markdown pad。

	mac下推荐mou。
	
+ ###gitcafe

	如果还没有赶紧去注册一个吧
	
	在你的电脑与 GitCafe 服务器之间保持通信时，我们使用 SSH key 认证方式来保证通信安全，所以在使用 GitCafe 前你必须先建创自已的 SSH key。
	
 1).进入SSH目录
 
	 cd ~/.ssh
如果还没有`~/.ssh`目录的话，请先手工创建一个`mkdir ~/.ssh`。
2).生成新的SSH秘钥
如果你已经有了一个秘钥（默认秘钥位置`~/.ssh/id_rsa` 文件存在），但是你想在 GitCafe 网站上使用另一套秘钥，请查看 [如何同时使用多个公秘钥](https://gitcafe.com/GitCafe/Help/wiki/%E5%A6%82%E4%BD%95%E5%90%8C%E6%97%B6%E4%BD%BF%E7%94%A8%E5%A4%9ddA%E4%B8%AA%E5%85%AC%E7%A7%98%E9%92%A5)

记得把以下命令中的 `YOUR_EMAIL@YOUREMAIL.COM` 改为你的 Email 地址(gitcafe绑定的Email)

	ssh-keygen -t rsa -C "YOUR_EMAIL@YOUREMAIL.COM"
	
3).生成过程中会出现以下信息，按屏幕提示操作，并记得输入 passphrase 口令。

	$ ssh-keygen -t rsa -C "YOUR_EMAIL@YOUREMAIL.COM"
	Generating public/private rsa key pair.
	Enter passphrase (empty for no passphrase):
	Enter same passphrase again:
	Your identification has been saved in /c/Users/	USERNAME/.ssh/id_rsa.
	Your public key has been saved in /c/Users/	USERNAME/.ssh/id_rsa.pub.
	The key fingerprint is:
	15:81:d2:7a:c6:6c:0f:ec:b0:b6:d4:18:b8:d1:41:48 	YOUR_EMAIL@YOUREMAIL.COM
	
*  SSH 秘钥生成结束后，你可以在用户目录 (~/.ssh/) 下看到私钥 id_rsa 和公钥 id_rsa.pub 这两个文件，记住千万不要把私钥文件 id_rsa 透露给任何人。


4).添加SSH公钥到GitCafe

 * 用文本工具打开公钥文件 `~/.ssh/id_rsa.pub` ，复制里面的所有内容到剪贴板。
 * 进入 GitCafe -->账户设置-->SSH 公钥管理设置项，点击添加新公钥 按钮，在 Title 文本框中输入任意字符，在 Key 文本框粘贴刚才复制的公钥字符串，按保存按钮完成操作。
 
 ![add_ssh_key](http://yangxiaolei.qiniudn.com/add_ssh_key.png)

***

5).测试链接

以上步骤完成后，你就可以通过以下命令来测试是否可以连接 GitCafe 服务器了。

	ssh -T git@gitcafe.com
	
如果是第一次连接的话，会出现以下警告，

	The authenticity of host 'gitcafe.com (50.116.2.223)' 	can't be established.
	#RSA key fingerprint is 84:9e:c9:8e:7f:36:28:08:7e:13:bf:43:12:74:11:4e.
	#Are you sure you want to continue connecting (yes/	no)?
	
	
请检查一下显示的指纹是否跟我们提供的一致： `84:9e:c9:8e:7f:36:28:08:7e:13:bf:43:12:74:11:4e`。
如果不一致请联系你的网络管理员，检查是否有中间人攻击。

如果没有问题，输入 `yes` 按回车就可以了。

中间会提示你输入 passphrase 口令。

最后，如果连接成功的话，会出现以下信息。

	Hi USERNAME! You've successfully authenticated, but 	GitCafe does not provide shell access.

* 到现在为止我们的准备工作做的差不多了

***

##3.下载hexo，制定自己的主题

我们可以去[hexo](http://hexo.io)官网去看看指导教程。

有时候会提示你错误，这时候你试试用root权限来执行你要执行的命令就会成功。

利用npm命令安装，在终端执行以下命令
	
	npm install hexo -g
	
如果执行了之后没反应，按Ctrl+c结束运行。然后再执行一遍安装命令。成功的话会出现以下提示

![](http://yangxiaolei.qiniudn.com/QQ20140621-1.png)

接下来cd到你准备放这个项目的空文件下执行下面这条命令：

	hexo init
	
![](http://yangxiaolei.qiniudn.com/屏幕快照 2014-11-30 下午5.46.13.png)
	
这条命令是初始化你这个文件夹如果一切顺利的话你去这个文件夹下去看看，会发现多了很多文件。


![](http://yangxiaolei.qiniudn.com/屏幕快照 2014-11-30 下午5.47.25.png)


文件夹的结构：

	.
	├── _config.yml
	├── package.json
	├── scaffolds
	├── scripts
	├── source
	|   ├── _drafts
	|   └── _posts
	└── themes
	
* deploy：执行hexo deploy命令部署到GitHub上的内容目录
* public：执行hexo generate命令，输出的静态网页内容目录
*   scaffolds：layout模板文件目录，其中的md文件可以添加编辑
  * scripts：扩展脚本目录，这里可以自定义一些javascript脚本
   * source：文章源码目录，该目录下的markdown和html文件均会被hexo处理。该页面对应repo的根目录，404文件、favicon.ico文件，CNAME文件等都应该放这里，该目录下可新建页面目录。
   * _drafts：草稿文章
   * _posts：发布文章
   * themes：主题文件目录
   * _config.yml：全局配置文件，大多数的设置都在这里
   * package.json：应用程序数据，指明hexo的版本等信息，类似于一般软件中的 关于 按钮

* 后边我们会讲到每个文件的作用。那么我们接着继续在终端中敲命令。

***

我们接下来执行这条命令，他会下载`package.json`的东西，这是我们所需要的，但是你不必太过于关心到底是做什么用的。

	npm install
	
执行成功的话你会看到下面的提示，并且在刚才的文件夹下又会多出现一个文件 `node_moudules` 这里面放的是我们会用的模版。

![](http://yangxiaolei.qiniudn.com/屏幕快照 2014-11-30 下午5.54.47.png)


***
接下来来的命令你就会看到 hello world 。是不是都等不急了？在终端中接着输入：

	hexo generate && hexo server
	
如果一切都还顺利的话，它会提示你打开`localhost:4000`，你就会看到hexo的界面了，看到的是官方默认的主题。

![](http://yangxiaolei.qiniudn.com/QQ截图20140621195119.png)


***



* 你是不是已经迫不及待的立马写一篇文章了？官方默认的第一篇博客，就是教你怎么去写一篇文章了。赶紧的，试试吧！

##在下一篇文章我们来继续探讨，尽请期待！







	
	
