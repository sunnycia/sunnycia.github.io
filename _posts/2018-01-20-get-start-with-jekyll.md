---
layout: post
title: "Get start with github jekyll blog"
author: "sunnycia"
categories: journal
tags: [documentation,sample]
image: jekyll.png
---

# Initial git repo
github 提供了一个很好的接口, 即如果你建立一个名为username.github.io的仓库(其中username是你的github用户名), github就会自动为你生成一个域名为username.github.io的网站. 刚开始我们可以尝试建立一个index.html, 并根据html的语法写一个简单的页面, push到github上之后就可以访问网站, 看到index中的内容了.你也可以使用css文件让你的页面更加美观.

顺带一提关于建github仓以及在本地同步的基本做法.可以直接在主页里点击make new repository, 建立一个名为username.github.io的仓库. 下一步在本地建立一个文件夹, 进入文件夹键入```git init```创建好本地的仓库, 然后在本地仓库下键入```git remote add origin https://github.com/yourusername/yourusername.github.io``` 同步远端仓库. (注意https和ssh方式的区别, 一种每次都要输入用户名和密码, ssh需要配置公钥和私钥, 不需要每次输入) 在本地仓库做了修改之后可以键入```git status```查看当前仓库的状态, ```git add --all```添加所有改动, ```git commit -m "description"```完成一次提交以及```git  push -u origin master```将本地仓库改动同步到远端仓库.

使用手打的html页面固然值得敬佩, 不过我们提倡重用, 如果有良好的静态页面模板, 帮我们生成美观的页面, 我们不用过多考虑页面语法, 配置完毕后就可以专注于写自己的po文, 那当然是极好的.所幸, jekyll就可以满足我们的愿望. 

# Install ruby->gem->jekyll

Jekyll是一个简易的静态网页生成器, 在本地部署jekyll可以方便我们对页面进行调试. 

pitfall: 之前我并没有部署jekyll, 直接下载好一个[模板](http://jekyllthemes.org/)后push到github上, 结果发现打开sunnycia.github.io页面并没有更新.开始以为是浏览器缓存的问题, 但是清理后发现并没有作用. 无意中发现在注册github的邮箱里收到了几封邮件,都是github page发来的错误提示, 这才明白为什么页面没有更新了. 本地有了jekyll之后我们就可以在目录下键入```jekyll server```, 尝试页面是否生成成功, 并且可以在浏览器中查看网页效果.

部署jekyll之前需要安装ruby, 可以进入ruby官网查看windows或linux系统下的安装方式. 我在centos下是使用源码编译安装.获得源码包ruby-2.3.x之后进入目录, 键入
```
bash configure &&
make && sudo make install
```
即可完成安装. 此时gem也同时安装成功, 可以通过```ruby -v && gem -v```查看版本信息

gem是与ruby绑定在一起的一个包管理工具, 作用类似于python的pypi或easy_install, 有了gem就可以方便地去获取其他人上传的基于ruby完成的工具了.

pitfall: 使用gem安装jekyll过程也很简单, 只需一个命令即可```gem install jekyll```     但是我键入这个命令后半天都没有反应, 查找资料了解到可以在命令后面附加```-V```选项观测安装情况. 由于默认的软件源 rubygems.org 比较慢, 所以会给人半天没有反应的感觉.解决办法也很简单, 就是换一个gem源.```gem source -l```查看当前的软件源, ```gem sources --remove https://rubygems.org/``` 移除旧的官方软件源, ```gem source -a https://ruby.taobao.org/```附加淘宝的gem软件源. 最后再用	```gem source -l```查看当前软件源, 确定只剩下了一个taobao软件源.

成功安装好jekyll之后就可以把下载好的模板里的文件全都copy到yourusername.github.io的目录下面, 然后在目录中键入```jekyll server```开启服务, 若有错误, 会有提示. 常见的问题有配置的错误或者缺少了依赖项.如果是缺少了依赖项可以使用```gem install```的方式安装它提示的缺失项.

tips:
jekyll-gist, pygments...


如果开启服务后没有问题, 则会提示server running. 这是你可以在浏览器中键入它显示的服务地址(默认为http://127.0.0.1:4000)来浏览生成的页面. 一般我们发一篇新的po文都是向模板里的_post目录下增加一个以日期命名的markdown文件, jekyll会根据md文件中头标记来判断该文章是否为一篇po文.具体可研究模板中的示例文件内部的写法. 一切无误后就可以将本地的仓库同步到远端, 向世界发布你的所思所想了~  

