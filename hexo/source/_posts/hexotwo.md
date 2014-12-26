title: 在Gitcafe搭建自己的博客(二)
date: 2014-12-02 11:06:21
categories: Git
tags: Hexo
---
##在上一篇博客我们已经在本地搭建好了环境，并且在本地也写好了第一篇博客。但是此时呢，你只能在本地的127.0.0.1:4000看到效果，那么接下来我们就要让别人也能够看到自己的博客，在才是我们真正的目的呀。
<!--more-->
***
###先让我写一篇博客吧
* cd到博客的根目录执行下边的命令：

	`hexo new "我的第一篇博客"`
	
在source/_posts 目录下就会生成一个.md的文件，我们就可以在这个文件里面使用markdown语法来写我们的博文了。如果你还不会markdown语法那就赶紧去百度一下吧，先去了解几个比较简单的。如果你实在不想用markdown的话，那你也可以把文件格式改成html，在接在html格式的文件里直接用html语法来写的你博客。

你一定会注意到在我的首页你只能看到这篇博客的一部分，如果你需要阅读全部的话需要点击Read More。如果你也要让一篇博客的部分在首页展示出来，其余的隐藏的话。在写博客的时候加上`<!--more-->
`那么在其上边的就会在首页显示出来，在其下边的地方在首页就会被隐藏。像下边这样子：

![](http://yangxiaolei.qiniudn.com/屏幕快照 2014-12-04 下午5.51.29.png)

* cd到博客的根目录执行下边的命令：

	 `hexo g && s`
	 
	 然后打开浏览器就可以看到你刚刚写的博客啦。
	
*  hexo g 这个命令是在本地生成静态文件，hexo d这个命令是将生成的静态文件同步到你的远程仓库中（gitcafe或者是github）
	*** 
##接下来才是关键。

###在gitcafe上先创建一个项目，这个项目的名称必须和你的用户名是一样的。例如我的gitcafe的用户名称是xiaole，所以我的这个项目的名称也是xiaolei。将来就可以通过your_name.gitcafe.com 来访问你的博客了。(如果你是在Github上的话，项目的名称类似于这样：yangxiaoleigithub.github.io。yangxiaoleigithub这是我的Github名称，通过your_name.github.io来访问)。



##我们再配置一些东西

>###在博客的根目录下有`_config.yml`这么一个文件，这就我们最为重要的配置文件了。请注意，每个属性名称和属性值之间都有一个空格，没有的话会出现错误，切记切记！！！！
	
	


	# Hexo Configuration
	## Docs: http://zespia.tw/hexo/docs/configure.html
	## Source: https://github.com/tommy351/hexo/

	# Site #整站的基本信息
	title: 一影成城 #网站标题
	subtitle: 码农，程序猿，未来的昏析师 #网站副标题
	description: bruce sha's blog | java | scala | bi #网站描述，给搜索引擎用的，在生成html中的head->meta中可看到
	author: bruce #网站作者，在下方显示
	email: bu.ru@qq.com #联系邮箱
	language: zh-CN #语言

	# URL #域名和文件结构
	## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
	url: http://ibruce.info #你的域名
	root: /
	permalink: :year/:month/:day/:title/
	tag_dir: tags
	archive_dir: archives
	category_dir: categories
	code_dir: downloads/code

	# Writing #写文章选项
	new_post_name: :title.md # File name of new posts
	default_layout: post #默认layout方式
	auto_spacing: false # Add spaces between asian characters and western characters
	titlecase: false # Transform title into titlecase
	external_link: true # Open external links in new tab
	max_open_file: 100
	multi_thread: true
	filename_case: 0
	render_drafts: false
	highlight: #代码高亮
  	enable: true #是否启用
  	line_number: false #是否显示行号
  	tab_replace:

	# Category & Tag #分类与标签
	default_category: uncategorized # default
	category_map:
	tag_map:

	# Archives #存档，这里的说明好像不对。全部选择1，这个选项与主题中的选项有时候会有冲突
	## 2: Enable pagination
	## 1: Disable pagination
	## 0: Fully Disable
	archive: 1
	category: 1
	tag: 1

	# Server #本地服务参数
	## Hexo uses Connect as a server
	## You can customize the logger format as defined in
	## http://www.senchalabs.org/connect/logger.html
	port: 4000
	logger: true
	logger_format:

	# Date / Time format #日期显示格式
	## Hexo uses Moment.js to parse and display date
	## You can customize the date format as defined in
	## http://momentjs.com/docs/#/displaying/format/
	date_format: MMM D YYYY
	time_format: H:mm:ss

	# Pagination #分页设置
	## Set per_page to 0 to disable pagination
	per_page: 10 #每页10篇文章
	pagination_dir: page

	# Disqus #社会化评论disqus，我使用多说，在主题中配置
	disqus_shortname:

	# Extensions #插件，暂时未安装插件
	## Plugins: https://github.com/tommy351/hexo/wiki/Plugins
	## Themes: https://github.com/tommy351/hexo/wiki/Themes
	## 主题
	theme: modernist # raytaylorism # pacman # modernist # light
	exclude_generator:

	# Deployment #部署
	## Docs: http://zespia.tw/hexo/docs/deploy.html
	### *下边两个你选一个，一个是往github提交静态页面的，一个是往gitcafe上，两个还是有点小区别的。
	deploy:
  	type: github
  	repository: git@github.com:bruce-sha/bruce-sha.github.com.git 
  	#你的GitHub Pages仓库


	(# 部署配置 ( 这个十分重要哦)
	## Docs: http://hexo.io/docs/deployment.html
	deploy:
	type: github
	repository: git@gitcafe.com:xiaolei/xiaolei.git
	branch: gitcafe-pages)
	
###上边就是全局的具体的一些配置，你还可以根据自己的喜好再稍有改动。

* 
###在这里说一下往github和gitcafes提交静态页面时的一些不同吧。

* 如果你是往github的话那就比较简单了，确定你全局配置文件配置没有问题，并且你的本地库可以和远程库连接上，那么你执行下边这两条代码就可以把你刚才写的博客上传了。并且可以通过类似于这样<http://yangxiaoleigithub.github.io>的URL格式来访问你问博客了。

	`hexo g`
	
 	`hexo d`
 
 ***
* 但如果你是往gitcafe的话那还稍有点麻烦了，因为默认的`master`分支不提供pages的功能(好像是这么回事)，官方给的方案是提交到`gitcafe-pages`分支下。那么你就要创建这个分支。

* 在你的hexo博客目录下面有一个隐藏的文件`.deploy`，请先cd到这个目下边然后执行下边的命令：
>创建gitcafe-pages分支，并切换到该分支
>
>`git checkout -b gitcafe-pages` 
>
>添加到gitcafe的远程仓库 
>
>`git remote add origin 'git@gitcafe.com:yourname/yourname.git`
>
>*push到gitcafe仓库(以后使用hexo g生成之后到.deploy目录执行即可)*
>
>`git push -u origin gitcafe-pages
`

* OK大功告成了。接下来切换到你的博客根目录，执行：



###`hexo g`

###`hexo d`

##这两个命令以后会经常用到哦。


###就可以通过`yourname.gitcafe.com`来访问你的博客了。

>###你坑定不满足于此，还想要自己喜欢的主题。下一篇我们就来说说，怎么配置一款自己喜欢的主题和一些其他的功能！