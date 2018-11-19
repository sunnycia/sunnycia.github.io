---
layout: post
title: "Establish a forward proxy on windows use wamp"
author: "sunnycia"
categories: journal
tags: [documentation,sample]
image: proxy.gif
---

# Try it on linux?
本文提供了在windows上搭建前向代理服务的一种解决方案，若是您想要在linux上完成该任务， 可以在linux平台下搭建基于squid的代理上网服务器，详细步骤可参考[这篇文章](http://zhengbo.site/squid-setup/)


# Start on Window

在考虑使用windows上搭建代理服务器之前， sunnycia使用的解决方案是用一台linux虚拟机配置好squid然后供服务器上网。可是好景不长，学校提供的上网帐号只允许在一个地方登录， 意味着若是linux虚拟机登录上网后，windows宿主机便无法正常上网。无奈之下只好寻找在windows下配置代理的方法， 经过尝试之后成功， 现将关键步骤记录如下。 本篇文章主要参考[这篇文章](https://blog.csdn.net/qq_29277155/article/details/53856455) 以及[这篇文章](https://blog.gtwang.org/web-development/apache-proxy/)

首先下载wamp， 一个在windows平台下配置apache，mysql以及php的综合平台。其实配置代理只需要apache服务器支持就够了，不过安装wamp能帮用户解决许多烦恼， 因此是一个不错的选择。若想要直接使用apache配置proxy server，请参考[这篇文章](https://blog.csdn.net/qq_29277155/article/details/53856455).

到[wamp官网](http://www.wampserver.com/en/)下载并安装[最近版本的wamp](https://sourceforge.net/projects/wampserver/files/latest/download).

默认安装完毕后在c盘根目录下找到安装根目录wamp64， 点击运行wampmanager.exe即可启动服务， 右下角的图标颜色为绿色表明所有服务启动正常。
![wamp success](../_assets/img/wamp_success.jpg)
此时在浏览器里打开localhost即可看到wamp生成的主页。
![wamp homepage](../_assets/img/wamp_homepage.jpg)

成功后进入wamp根目录下的bin/apache/apache2.*.*文件夹下， 或者单击右下角的wamp图标，修改apache的httpd.conf配置文件

需要取消注释(uncomment)掉几个扩展配置:proxy\_module，proxy\_module，proxy\_http\_module，proxy\_ftp\_module，修改后这几行应为：
--------------------- 
LoadModule proxy\_module modules/mod_proxy.so
LoadModule proxy\_connect\_module modules/mod\_proxy\_connect.so
LoadModule proxy\_http\_module modules/mod\_proxy\_http.so
LoadModule proxy\_ftp\_module modules/mod\_proxy\_ftp.so
---------------------


然后在httpd.conf文件最后附上：
ProxyRequests On
ProxyVia On

<Proxy *>
Order deny,allow
Deny from all
Allow from internal.example.com
</Proxy>
其中 internal.example.com换成你允许使用该proxy上网的ip地址。

完成后restart wamp， 若wamp图标变为绿色，即表明配置成功
