title: 在Gitcafe搭建自己的博客(三)
date: 2014-12-04 18:11:32
categories: Git
tags: Hexo
---
#接下来我们来改变我们Hexo的主题吧，好在官方已经给我们准备好了大量的Hexo的主题。
<!--more-->
##[官网主题链接使劲戳进来!](https://github.com/hexojs/hexo/wiki/Themes)

###到这里找到你喜欢的主题吧，如果你还有些不满足还可以根据自己的情况加以修改。

* ### 把你喜欢的主题下载到本地之后解压放在`themes`这个目录下边就可以了，你可以把这个主题的文件夹名字命名成你自己喜欢的。还记得全局配置文件吗？在你的hexo跟目录下有个`_config.yml`,在这里面你需要去修改一下主题，改成你的主题名称，保存退出。(切忌你的主题名字和theme:之间一定要有一个空格，否则会有错误)

>	
	## Plugins: https://github.com/hexojs/hexo/wiki/Plugins
	## Themes: https://github.com/hexojs/hexo/wiki/Themes
	theme: 你的主题文件夹名称
	exclude_generator:
	
* ###接下来你再去配置一下你的主题的配置文件，在你的主题的目录下也有一个`_config.yml`文件。在里边可以配置你的主题的一些选项。又可能每个主题的配置文件有点不一样。
```
.
├── languages          #多语言
|   ├── default.yml    #默认语言
|   └── zh-CN.yml      #中文语言
├── layout             #布局，根目录下的*.ejs文件是对主页，分页，存档等的控制
|   ├── _partial       #局部的布局，此目录下的*.ejs是对头尾等局部的控制
|   └── _widget        #小挂件的布局，页面下方小挂件的控制
├── source             #源码
|   ├── css            #css源码 
|   |   ├── _base      #*.styl基础css
|   |   ├── _partial   #*.styl局部css
|   |   ├── fonts      #字体
|   |   ├── images     #图片
|   |   └── style.styl #*.styl引入需要的css源码
|   ├── fancybox       #fancybox效果源码
|   └── js             #javascript源代码
├── _config.yml        #主题配置文件
└── README.md          #用GitHub的都知道
```
* ####如果你需要给你的博客添加评论的功能的话，就会用到多说插件，Hexo原本默认的评论插件在天国不能使用，原因你懂得。国内的多说也是非常的潮流的，用起来也很方便。下边列出我的主题的配置文件可以参考看看。




	```
	menu:

	首页: /
  	
  	博客: /archives
  	关于我: /about

	widgets:
	# 配置页脚显示哪些小挂件
	- search
	- category
	- tag
	- recent_posts
	- tagcloud
	cover:
 	 enable: true
  	url: http://bcs.duapp.com/xiaoleihexo/banner.jpg
   
	excerpt_link: Read More

	full_format: 'ddd, MMM D YYYY, h:mm:ss a'

	addthis:
  	enable:
  	pubid:
  	facebook:
  	twitter:
  	google: 
  	pinterest:

	fancybox: true

	google_analytics: UA-368771XX-X
	rss:

	comment_provider: duoshuo

	# Duoshuo comment
	duoshuo:
  	short_name: yangxiaoleicom(多说short_name)

	social:
  	github: https://github.com/yangxiaoleigithub
  	weibo: http://weibo.com/xiaoleiswift
  	google_plus: 

  	# 友情链接
  	blogrolls:
  	# - bruce sha's javaeye: http://buru.iteye.com

	auto_change:
  	enable: true
```



###**评论框**

静态博客要使用第三方评论系统，hexo默认集成的是 Disqus,所以国内的话还是建议用 多说 。
直接用你的微博/豆瓣/人人/百度/开心网帐号登录多说，做一下基本设置。如果使用modernist主题，在 modernist_config.yml 中配置duoshuo_shortname为多说的 基本设置->域名中的shortname即可。你也可以在多说后台自定义一下多说评论框的格式，比如评论框的位置，对于css设置，可以 [参考这里](http://dev.duoshuo.com/docs/4ff1cfd0397309552c000017) 。

如果你是有的其他第三方评论系统，将通用代码粘贴到 hexo\themes\modernist\layout\_partial\comment.ejs 里面，如下： 

	<% if (config.disqus_shortname && page.comments){ %>
	<section id="comment">
 	 #你的通用代码
	<% } %>
	
###**自定义页面**

执行new page命令

	

	hexo new page "about"
	
在 hexo\source\ 下会生成 about 目录，里面有个index.md，直接编辑就可以了，然后在主题的 _config.yml 中将其配置显示出来。
上述步骤，也可以手工生成，在 hexo\source\ 下手工新建 about 和 index.md 也是完全等价的。 


>因为markdown对table的支持不好，我是在about中直接建立index.html，里面书写页面内容，hexo会帮你加上头和尾。


###**404页面**

GitHub Pages [自定义404页面](https://help.github.com/articles/custom-404-pages/) 非常容易，直接在根目录下创建自己的 404.html 就可以。但是自定义404页面仅对绑定顶级域名的项目才起作用，GitHub默认分配的二级域名是不起作用的，使用 hexo server 在本机调试也是不起作用的。 


###**图床**
考虑到博客的速度，同时也为了便于博客的迁移，图床是必须的。我墙裂推荐七牛，访问速度极快，支持日志、防盗链和水印。

免费用户有每月10GB流量+总空间10GB+PUT/DELETE 10万次请求+GET 100万次请求，这对个人博客来说足够，不够的话点这个活动页面，也可通过邀请好友获得奖励，我[邀请一下 七牛邀请](https://portal.qiniu.com/signup?code=3lqg1xvako382) 。有一点要说明的是，七牛没有目录的概念，但是文件名可以包含 / ，比如 2013/11/27/reading/photos-0.jpg ，参考这里 [关于key-value存储系统](http://kb.qiniu.com/key-value-system) 。 

  
七牛除了作为图床还可以作为其他静态文件存储空间，比如我的个人站点首页有个字库文件和JS文件下载较慢，有时间会把它弄到七牛上去，以提高首页打开速度。请看这篇[ Linux中国采用七牛云存储支撑图片访问](http://linux.cn/thread/11986/1/1) 。


####您还可以使用如下图床服务 [FarBox](https://www.farbox.com/) ， [又拍云](https://www.upyun.com/index.html) 。 



####**申请域名（可选）**
GitHubPages默认为每个用户分配了一个二级域名『your_user_name.github.com』或『your_user_name.github.io』。

如果你对上述域名不满意，可以到[万网](http://www.net.cn/)上申请一个自己的域名，然后绑定到GitHub Pages。绑定方法很简单，在souce目录下建立一个CNAME文件，里面写上域名并提交即可。 在万网解析域名，ip写github活着gitcafe提供的IP。
***

####**命令**
```
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #将.deploy目录部署到GitHub
```

####**简写**
```
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
```

##**在此我要给上一些链接，感谢他们。很多地方都是参考他们的，他们还有很多好的博文大家也可以去看看。**


1. <http://www.tuicool.com/articles/AfQnQjy>
2. <http://blog.maxwi.com/2014/03/20/learn-mardown-in-5-minutes/>
3. <http://www.jianshu.com/p/31cbbbc5f9fa/>
4. <http://blog.maxwi.com/2014/03/19/hexo-github-to-gitcafe/>
5. <http://www.liaoxuefeng.com/>
	
	>也许你和我一样会遇到很多麻烦，可以给我发邮件一起来探讨。
	由于水平有限，可能会存在很多错误，还希望你发现后给我留言或者发邮件提醒。
	感谢这么多开源的技术，这么多免费的平台。







