---

layout: post

title: "如何在ubuntu server上安装图形界面并配置lamp和phpmyadmin"

keywords: ubuntu server，图形界面，lampp

description: 在ubuntu server上安装图形界面并配置lamp和phpmyadmin

date: 2016-12-21 22：00

author: "尹傲雄"

categories: [linux]

---
在安装完ubuntu server之后，发现它默认是没有图形界面的，于是就想安装一个，虽然命令行功能强大，作为一个小白还是没怎么习惯，而且感觉一些简单的操作用图形化的界面还是要方便一点的
安装图形界面的命令如下：

```
sudo apt-get update //更新软件列表

sudo apt-get upgrade//更新软件

sudo apt-get install ubuntu-desktop
```
安装其他的桌面

```
sudo apt-get install --no-install-recommends ubuntu-desktop//不带应用软件的桌面
sudo apt-get install xubuntu-desktop//安装轻量级桌面 xfce
sudo apt-get install kubuntu-desktop
安装 KDE 桌面
```
如果选的是不带应用的桌面的话，连浏览器都是没有的，所以很不方便可以使用以下命令安装google浏览器：`sudo apt-get install chromium-browser`

然后就是配置lamp环境啦，步骤如下：

 1. 首先安装apache2：在终端输入`sudo apt-get install apache2`
这时在虚拟机的浏览器中输入local host如果能见到以下界面说明安装成功。
![这里写图片描述](http://img.blog.csdn.net/20161221131557660?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWluYW94aW9uZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
 2. 然后就是安装php了，使用`sudo apt-get install php`安装php，默认安装的是php7，而且官方的源里没有php5，不过实在是有需要的话可以自己换一个ppa的源，输入`php -v`显示如下情景说明安装正确。![这里写图片描述](http://img.blog.csdn.net/20161221221409689?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWluYW94aW9uZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
 3. 然后就是安装mysql-server了，输入`sudo apt-get install mysql-server`就可以了，然后按照提示设置你的数据库密码。
 4. 然后安装phpmyadmin，输入`sudo apt-get install phpmyadmin`按照提示选择apache2，按照提示输入数据库的密码就是了，与数据库建立连接。

 到这里要安装的就都安装好了。接下来就是一些配置了，更改一下/var/www这个文件夹的权限，输入`sudo chmod 777 /var/www -R`将其权限改为可读可写可执行。这时你在浏览器输入localhost/phpmyadmin的话会发现一个404错误，这时输入`sudo ln -s /usr/share/phpmyadmin /var/www/html/`创建一个链接就可以了。再次输入结果发现虽然没有404错误但是显示的是一堆代码如下图所示：![这里写图片描述](http://img.blog.csdn.net/20161222221024744?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWluYW94aW9uZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
 登录界面无法显示直接显示php代码。查找资料发现是忘了安装apache的php拓展，apache无法显示php页面，运行下面的命令`sudo apt-get install libapache2-mod-php7.0`之后就可以正确显示了。好了基本的配置就完成了。
