---
layout:     post
title:      个人博客搭建
subtitle:   用wordpress从零开始搭建个人博客
date:       2019-8-17
author:     LGT
header-img: img/post-bg1.png
catalog: true
tags:
    - blog
    - 零基础
    - 教程
---

# 个人blog搭建

[TOC]

## 一、购买自己的服务器

​	在阿里云或者腾讯云买一个，一般都会有学生优惠，大概10rmb/月，还是很实惠的。预装系统可以选CentOS、Ubuntu和Windows。看个人需求和喜好吧。如果不大清楚的话可以选CentOS，这篇教程后面也是按照CentOS的系统进行的。（购买之后也还可以更换系统，所以不必太纠结）

​	购买完成后在实例列表中找到自己的公网IP，以后就可以通过这个IP访问到服务器了：![QQ截图20190817111927](http://47.103.197.224/wordpress/wp-content/uploads/2019/08/QQ%E6%88%AA%E5%9B%BE20190817111927.png)



## 二、为服务器搭建LAMP环境

### 工具介绍

​	购买完服务器之后就可以着手搭建我们的LAMP环境了，不过先不着急。我们需要先准备好两个软件：PuTTY和Xftp 6

​	PuTTY可以用来远程连接我们的服务器，Xftp可以用来在向我们的服务器传输文件。

​	PuTTY的界面是这样的：

![QQ截图20190817110806](http://47.103.197.224/wordpress/wp-content/uploads/2019/08/QQ截图20190817110806.png)

在HostName(or IP address)输入自己服务器的公网IP，然后点击open，就可以进行连接了：

![QQ截图20190817110843](http://47.103.197.224/wordpress/wp-content/uploads/2019/08/QQ截图20190817110843.png)

Xftp也差不多：

![QQ截图20190817111548](http://47.103.197.224/wordpress/wp-content/uploads/2019/08/QQ截图20190817111548.png)

### 搭建LAMP

工具讲解完了，可以开始搭我们的LAMP了。首先这里的LAMP指的是Linux+Apache+MariaDB+PHP

用PuTTY连接好我们的服务器以后

#### 安装Apache

安装Apache：

```shell
sudo yum install httpd
```

启动Apache：

```shell
sudo systemctl start httpd.service
```

启动之后就可以在浏览器中打开http://xxx.xxx.xxx.xxx/ 访问我们的网页了

如果访问不成功的话可以在阿里云的安全组规则看下服务器的80端口有没有开放

Apache服务器的网站文件默认在/var/www目录

#### 安装MariaDB

安装MariaDB：

```shell
sudo yum install mariadb-server mariadb
```

启动MariaDB：

```shell
sudo systemctl start mariadb
```

安装数据库安全脚本，去除一些危险的默认设置：

```shell
sudo mysql_secure_installation
```

然后根据提示进行一系列的设置就行

#### 安装PHP

CentOS yum默认安装的php的版本是5.4的，远远不够，这里我们要安装php7.2的版本

获取rpm：

```shell
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm   
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm 
```

安装PHP：

```shell
sudo yum -y install php72w php72w-cli php72w-common php72w-devel php72w-mysql php72w-gd php72w-imap php72w-ldap php72w-odbc php72w-pear php72w-xml php72w-xmlrpc
```

安装完成后输入php -v查看php版本信息：

![QQ截图20190817115106](E:\markdown\个人blog搭建.assets\QQ截图20190817115106.png)

安装完毕

然后在/var/www/html目录下新建一个info.php文件，编辑内容为：

```php
<?php phpinfo();?>
```

并用浏览器打开网页http://xxx.xxx.xxx.xxx/info.php （xxx.xxx.xxx.xxx为你的公网IP）

![QQ截图20190817115620](E:\markdown\个人blog搭建.assets\QQ截图20190817115620.png)

出现这个页面说明大功告成！

#### 安装phpMyAdmin

LAMP搭完以后，可以再安装一个phpMyAdmin，它是管理MariaDb数据库的Web界面程序，可以方便数据库的管理

安装EPEL库：

```shell
sudo yum install epel-release
```

安装phpMyAdmin：

```shell
sudo yum install phpmyadmin
```

设置phpMyAdmin的httpd设置，打开/etc/httpd/conf.d/phpMyAdmin.conf：

```
Alias /phpMyAdmin /usr/share/phpMyAdmin
Alias /phpmyadmin /usr/share/phpMyAdmin
<Directory /usr/share/phpMyAdmin/>
   AddDefaultCharset UTF-8
   <IfModule mod_authz_core.c>
     # Apache 2.4
     <RequireAny>
       Require ip 127.0.0.1
       Require ip ::1
     </RequireAny>
   </IfModule>
   <IfModule !mod_authz_core.c>
     # Apache 2.2
     Order Deny,Allow
     Deny from All
     Allow from 127.0.0.1
     Allow from ::1
   </IfModule>
</Directory>
```

将其修改为：

```
<Directory /usr/share/phpMyAdmin/>
   AddDefaultCharset UTF-8
   <IfModule mod_authz_core.c>
     # Apache 2.4
     <RequireAny>
       #Require ip 127.0.0.1
       #Require ip ::1
        Require all granted
     </RequireAny>
   </IfModule>
   <IfModule !mod_authz_core.c>
     # Apache 2.2
     Order Deny,Allow
    # Deny from All
    # Allow from 127.0.0.1
    # Allow from ::1
      Allow from All
   </IfModule>
</Directory>
```

重启Apache服务器：

```shell
sudo systemctl restart httpd.service
```

然后通过http://xxx.xxx.xxx.xxx/phpmyadmin访问phpMyAdmin，用mariadb的账号登录后，为wordpress创建一个数据库：

![QQ截图20190817132217](http://47.103.197.224/wordpress/wp-content/uploads/2019/08/QQ截图20190817132217.png)

![QQ截图20190817132243](http://47.103.197.224/wordpress/wp-content/uploads/2019/08/QQ截图20190817132243.png)

## 三、使用wordpress搭建个人博客

wordpress是一个较为成熟的博客框架，即使你不会php也可以使用wordpress搭建你的个人博客

首先，下载wordpress安装包：

```shell
wget http://wordpress.org/latest.tar.gz
```

然后解压并拷贝到/var/www/html/wordpress目录

```shell
tar xzvf latest.tar.gz
sudo rsync -avP ~/wordpress/ /var/www/html/wordpress/
```

然后浏览器打开http://xxx.xxx.xxx.xxx/wordpress 进行一些设置（大概就是填写你的数据库名称和数据库的账号密码之类的信息，数据库名称填之前创建的wordpress，账号填root就行）

创建结束之后就会进入到wp-admin，

 ![QQ截图20190817133259](http://47.103.197.224/wordpress/wp-content/uploads/2019/08/QQ截图20190817133259.png)

这里就是你的博客的后台，你可以随意探索，发布你的文章了。

## 四、装饰一下博客

​	觉得刚搭好的博客不太好看？想要装饰一下？你可以通过更换wp的主题来改变你的博客的亚子。wordpress提供了一些官方主题，如果看到喜欢的可以直接下载使用。当然你也可以自定义主题。

​	这里只是给出一个大致的思路，如果想深入了解wp的主题开发可以看官网的文档或者网上的一些资料，这里推荐一个b站上的视频教程：av48784295，up主的声音很好听hhh

​	首先在wordpress/wp-content/themes的目录下存放的是wp的主题样式，默认的有twentynineteen等三个主题，你可以在网上找一些wp的主题然后进行一些修改，也可以自己创建一个主题文件夹，然后进行主题的开发。

​	我的blog用的是[L-Talk](https://github.com/limileo/L-Talk )的主题进行开发，如果你们喜欢的话也欢迎去给原作者star哦！

