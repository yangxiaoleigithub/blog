title: PHP+Apache+Mysql+phpMyAdmin的配置
date: 2014-12-05 21:16:00
categories: PHP
tags: Mysql  
---
##今天突然想学习一下php这个十分受欢迎的后台服务器脚本，要想学习先要有环境吧。下边就介绍一下具体的环境配置吧。
<!--more-->
###因为mac上本来就有php和apache的环境，这样的话就少了我很多的事情。但还是需要一些简单的配置。

###一.配置Apache
**1.启动Apache**


打开终端，输入：
`sudo apachectl start`

打开浏览器，输入：`http://localhost`

应该可以看到“It works！”的页面，该页面位于/Library/WebServer/Documents/目录下，这是Apache的默认根目录。

**2.配置用户访问目录**

你可以修改他的默认跟目录
	
在终端中输入：mkdir ~/Sites

(Sites是你自己设置的跟目录的路径)

再输入：`sudo vim /etc/apache2/httpd.conf`

找到**/Library/WebServer/Documents（有两处)**

将其替换为**你自己设置的根目录**。

可以先在你设置的跟目录下新创建一个.php文件文件内容：

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>hello world</title>
</head>
<body>
	<?php
	echo"<h1>Hello World</h1>";
	?>	
</body>
</html>
```

**3.保存文件，运行：**

`
sudo apachectl restart
`

重启Apache,此时可以在浏览器中访问：

`http://localhost`

输出：
###Hello World

###二.配置PHP

在终端中输入：

`sudo vim /etc/apache2/httpd.conf`

找到下边这行代码：

`#LoadModule php5_module libexec/apache2/libphp5.so`

删除前面的#，然后保存退出。（按shift+i行首输入，按ESC退出编辑，按x删除当前字符，及#，输入:wq，保存并退出。）

在终端输入：

```
cd /etc

sudo cp php.ini.default php.ini

sudo apachectl restart
```

三.安装Mysql

1.mysql下载地址<http://dev.mysql.com/downloads/mysql/>

选择适合你电脑的版本

我刚开始的时候下载的是.dmg格式的，可是安装到最后一步的时候总是提示我莫名其妙的错误。到现在我还没有太弄明白

所以最后我下载的是.gz压缩包格式的。

###首先先介绍压缩包形式的安装方法：

```
 sudo mv mysql-5.1.45-osx10.6-x86_64 /usr/local/mysql
 cd /usr/local
 sudo chown -R mysql:mysql mysql
 cd mysql
 sudo scripts/mysql_install_db --user=mysql
 sudo chown -R root .
 sudo chown -R mysql data
```
 然后cd bin用

 `sudo ./mysql_secure_installation `

 来修改root密码，默认为空，显然不太安全。

`sudo ./mysqld_safe `

启动mysql

`sudo ./mysql -u root -p`

输入刚才设置的root密码来登录mysql

`sudo ./mysqld_safe stop`

停止mysql


###安装包文件形式的安装方法：

 首先，去<http://www.mysql.com/downloads/mysql>下载mysql-5.6.10-osx10.7-x86_64.dmg，然后，双击该文件，安装映像中的两个安装包文件。

a. mysql-5.6.10-osx10.7-x86_64.dmg（mysql标准版安装）

b. MySQLStartupItem.pkg（mysql启动项目）

可以在你电脑启动系统时自动运行mysql服务,它安装在/Library /StartupItems/MySQL/，如果你不想系统启动时运行mysql服务，请不要安装。如果你在安装后又不想使用，请删除/Library /StartupItems/MySQL/这个目录。

启动mysql服务

1、如果你已经安装了MySQLStartupItem.pkg，重新启动电脑即可。

2、如果你有安装MySQLStartupItem.pkg或者不想启动电脑，在终端中输入命令：

`sudo /Library/StartupItems/MySQLCOM/MySQLCOM start`

然后输入你的系统管理员密码即可。

关闭mysql服务

终端中输入命令：

`sudo /Library/StartupItems/MySQLCOM/MySQLCOM stop`

然后输入你的系统管理员密码即可。

####你也可以去系统偏好设置－其他－MySQL，通过这个来启动和停止MySQL服务。

###更改mysql root账户密码

 终端中输入命令：

 `/usr/local/mysql/bin/mysqladmin -u root password 新密码`


你可以随时使用这条命令更改你的密码。



###终端登录mysql

**方法1:绝对路径**

终端中输入命令：`/usr/local/mysql/bin/mysql -u root -p`

提示：输入你的新密码


**方法2：（推荐)相对路径**

终端中输入命令：

查看路径中有没有需要的路径：

终端中输入命令：`echo $PATH`

没有，继续

添加需要路径：`PATH="$PATH":/usr/local/mysql/bin`

以后

终端中需输入命令：`mysql -u root -p` 即可

###二.创建用户 分配权限 


**1.新建用户。 **

登录MYSQL 

`mysql -u root -p `

密码 

创建用户 

`mysql> insert into mysql.user(Host,User,Password) values("localhost","phplamp",password("1234")); `

刷新系统权限表

`mysql>flush privileges; `

这样就创建了一个名为：phplamp  密码为：1234  的用户。 

然后登录一下。 

`mysql>exit; `

`mysql -u phplamp -p `

输入密码 




**2.为用户授权。** 

登录MYSQL（有ROOT权限）。
`mysql -u root -p `

密码 

首先为用户创建一个数据库(phplampDB)

mysql>create database phplampDB;

授权phplamp用户拥有phplamp数据库的所有权限。

`>grant all privileges on phplampDB.* to phplamp@localhost identified by '1234'; `

刷新系统权限表 

`mysql>flush privileges; `

`mysql>其它操作` 


如果想指定部分权限给一用户，可以这样来写:

`mysql>grant select,update on phplampDB.* to phplamp@localhost identified by '1234';`

//刷新系统权限表。 

`mysql>flush privileges; `


3.删除用户。

`mysql -u root -p `
密码 

`mysql>DELETE FROM user WHERE User="phplamp" and Host="localhost"; `

`mysql>flush privileges; `

//删除用户的数据库 

`mysql>drop database phplampDB; `

4.修改指定用户密码。

`mysql -u root -p` 
密码

`mysql>update mysql.user set password=password('新密码') where User="phplamp" and Host="localhost"; `

`mysql>flush privileges; `

###最后一项下载phpMyAdmin来方便的管理数据库。

phpMyAdmin的[官方网站](http://www.phpmyadmin.net/home_page/index.php),来下载对应的版本。

1.下载后把解压后的文件夹放在你的apache的跟目录下

2.配置config文件 
  
  打开libraries下的config.default.php文件，依次找到下面各项，按照说明配置即可：

 **A** 查找 `$cfg['PmaAbsoluteUri']=''; `  // 修改为你将上传到空间的phpMyAdmin的网址 
如：`$cfg['PmaAbsoluteUri'] =‘http:   // 网站域名/phpmyadmin/'; `

**B**查找 `$cfg['Servers'][$i]['host'] =‘localhost'; `   // 通常用默认，也有例外，可以不用修改 

查找 `$cfg['Servers'][$i]['auth_type'] =‘config'; `  // 在自己的机子里调试用config；如果在网络上的空间用cookie.

在此有四种模式可供选择：cookie，http，HTTP，config

① config 方式即输入phpMyAdmin 的访问网址即可直接进入，无需输入用户名和密码，是不安全的，不推荐使用。 

② 设置cookie，http，HTTP方式，登录 phpMyAdmin 需要数据用户名和密码进行验证。

具体如下：PHP 安装模式为 Apache，可以使用 http 和 cookie；PHP 安装模式为 CGI，可以使用 cookie。  

**C**查找 `$cfg['Servers'][$i]['user'] = ‘root';`   // MySQL用户名 

`查找 $cfg['Servers'][$i]['password'] ='';  ` // MySQL 密码 

**D**查找 `$cfg['DefaultLang'] = ‘zh';  ` // 这里是选择语言，zh代表简体中文的意思

查找`$cfg['blowfish_secret'] =''; `  // 如果认证方法设置为cookie，就需要设置短语密码，设置为什么密码，由您自己决定，这里不能留空，否则会在登录 phpMyAdmin 时提示错误。


> 设置完成之后保存，浏览器中输入`http://localhost/phpMyAdmin`测试一下

>我当时遇到了＃2002错误，到网上查找后这样修改就没有错了。

>将 `“phpMyAdmin/libraries”`文件夹下的`config.default.php`文件中的

> `$cfg['Servers'][$i]['host'] = 'localhost';`

>修改为

>`$cfg['Servers'][$i]['host'] = '127.0.0.1';`

 

>就解决了。

>感到好奇怪，他这里给了解释：<http://www.cnblogs.com/sunzhenchao/archive/2013/01/16/2863160.html>


















