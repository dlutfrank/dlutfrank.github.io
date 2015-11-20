---
layout: post
title: 在Github上搭建博客
date: 2015-10-29 13:21:00
categories: blog
excerpt: 在github上搭建静态的博客
---

* content
{:toc}

一直以来都想搭建一个属于自己的博客，在上面放一些自己东西，搭建博客虽说不是很难，但还是繁琐，需要自己去购买虚拟服务器、购买域名、将博客程序部署在虚拟服务器上，搭建完成后维护的工作也并不轻松，对于我这种比较懒的人来说简直不能忍受。工作过程中，接触Github有了一段时间，在浏览的时候发现Github上能托管自己的博客，稍微了解了一下，发现对于码农来说，让博客run起来比以前容易多了。于是，在工作之余，抽出空闲时间，搭建了自己的博客。

---

## 搭建过程

### 准备

搭建博客过程中必须要用到的有 `git`，和`Github账号`，git可以直接去[git官网](http://git-scm.com/download/)下载，Github账号需要在[Github](https://github.com)上面注册。Github的博客系统使用的是`jekyll`的引擎，为了方便调试，最好在本地安装一个[jekyll](http://jekyll.bootcss.com/)。

### 流程

整个流程分为注册Github账号，搭建本地博客环境，撰写博文，将文章推送到Github等几个步骤。

#### 注册账号

注册Github账号相当简单，直接在[Github主页](https://github.com)进行注册即可。

#### 建立远程仓库

注册完后，需要[新建](https://github.com/new)一个特定的仓库来保存博客，该仓库的名称必须是`username.github.io`,`username`为注册Github时候的用户名，访问博客的时候，使用域名`username.github.io`就能访问了。

#### 克隆仓库

在Github上创建仓库后，需要将仓库clone到本地，以便在本地使用自己顺手的工具来撰写文章，然后推送到Github上，这里需要用到git来操作仓库，从Github上clone仓库到发布博文的步骤如下：

    $git clone https://github.com/username/username.github.io.git
	$cd username.github.io
	$echo "my blog" > index.html
	$git add .	
	$git commit -m "add blog file"
	$git push origin master

做完这些步骤后，就能通过博客的域名访问你刚才推送的index.html网页了。
	
如果每次写文章的时候都需要自己写html文件，将会相当麻烦，幸好Jekyll引擎能解析Markdown编写的文件，所以我们只需要用Markdown编写好文章，然后推送到博客仓库就可以了。

#### 搭建本地环境

为了更方便的在本地预览博客，可以在本地安装Jekyll,安装Jekyll也相当简单，只需要在终端输入

    $gem install Jekyll

就会自动安装Jekyll了，为了和Github上Jekyll环境保持一致，可以键入以下命令

    $gem install github-pages

搭建完本地环境后，可以使用Jekyll按以下步骤创建博客框架

    $cd username.github.io
	$jekyll new .

这时username.github.io文件夹中会多出这些文件和文件夹。

    _config.yml    整个系统的配置文件
	_includes      放头文件的文件夹，一般会被_layouts文件夹中的文件使用
	_layouts       放布局文件的文件夹，写文章的时候采用里面的布局文件
	_posts         放文章的文件夹	
	_site          jekyll生成的站点文件夹，可以不推送到远程仓库
	_index.html    博客系统主页面

用终端进入username.github.io文件夹，输入

    $jekyll serve

就会启动本地的博客服务器，通过浏览器访问[博客](http://localhost:4000)就可以看到jekyll创建博客的主页了。

为了让自己的博客看起好看一点，可以在网上搜索一下各种Jekyll theme，然后应用在自己的博客上，[Jekyll Themes](http://jekyllthemes.org)上面提供了很多主题,我这里使用的是[HyG的博客](https://github.com/Gaohaoyang/gaohaoyang.github.io)的主题。

#### 撰写博文

博客搭建完了后只需要将文件放在\_post文件夹中，同步到远程仓库，就可以通过浏览器访问了，\_post文件夹中的文件名必须符合`2015-11-3-file-name.md`这样的格式才会被视为有效的文件。

#### 发布文章

每次将文章添加到\_post文件夹中后，通过git将文章从本地同步到Github来实现发布新的文章。

    $git add .
	$git commit -m "new paper"
	$git push origin master

---

## 参考文章

* [Github Pages](https://pages.github.com/)
* [Github Pages Basics](https://help.github.com/categories/github-pages-basics/)
* [HyG的博客](https://gaohaoyang.github.io)
* [How Jekyll Works](http://jekyllbootstrap.com/lessons/jekyll-introduction.html)
* [Jekyll Themes](http://jekyllthemes.org/)
