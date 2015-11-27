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

搭建博客过程中必须要用到的有 `git`，和`Github账号`，git可以直接去[git官网](http://git-scm.com/download/)下载，Github账号需要在[Github](https://github.com)上面注册。Github的博客系统使用的是`jekyll`的引擎，为了方便本地调试，最好在本地安装一个[jekyll](http://jekyll.bootcss.com/)。安装jekyll并不是必须的，如果嫌麻烦可以不安装。

### 流程

核心流程分为注册Github账号，在Github上建立博客仓库，撰写博文，将文章推送到Github等几个步骤，整个流程可以参考[Pages官网](https://pages.github.com/)。

#### 注册账号

注册Github账号相当简单，直接在[Github主页](https://github.com)进行注册即可。

#### 建立远程仓库

注册完后，需要[新建](https://github.com/new)一个特定的仓库来保存博客，该仓库的名称必须是`username.github.io`,`username`为注册Github时候的用户名，访问博客的时候，使用域名`username.github.io`就能访问了。

#### 克隆仓库

在Github上创建仓库后，需要将仓库clone到本地，以便在本地使用自己顺手的工具来撰写文章。

    $git clone https://github.com/username/username.github.io.git

#### 发布主页

进入本地博客根目录，创建index.html文件，然后推送到远程仓库中。

	$cd username.github.io
	$echo "my blog" > index.html
	$git add .	
	$git commit -m "add blog file"
	$git push origin master

做完这些步骤后，就能通过博客的域名访问你刚才推送的index.html网页了，至此，搭建博客就算初步完成了。但是，如果发布博客的时候，每次写文章都需要写html文件，同时编辑index文件来导航到我们的每一篇文章，将会相当麻烦，幸好Jekyll将这两个难题都解决了。我们可以在本地编写符合Jekyll规范的网站源码，然后上传的Github上，这样就能够简单方便的发布博文了。

### 创建Jekyll规范的站点

为了方便撰写博客文章，同时也为了方便对文章进行管理，我们需要创建符合Jekyll规范的站点,Jekyll最主要的文件和文件夹如下：

    _config.yml    整个系统的配置文件
	_includes      放头文件的文件夹，一般会被_layouts文件夹中的文件使用
	_layouts       放布局文件的文件夹，写文章的时候采用里面的布局文件
	_posts         放文章的文件夹	
	index.html    博客系统主页面

`_config.yml`文件为博客网站系统的配置文件，在该文件中可以设置一些变量，然后写博客的时候就可以直接引用了。例如配置变量`title:myblog`，在博客中就可以通\{\{site.title\}\}访问该变量。

`_includes`文件夹中存放一些被其他文件引用的公共文件，主要是为了模块化和统一风格用。例如可以新建一个head.html的文件来控制页面标题的显示，内容如下：

> \<head\>
>
   \<meta charset="utf-8"\>
>
   \<title\>\{ % if page.title %\}\{\{ page.title \}\}\{ % else %\}\{\{ site.title \}\}\{ % endif %\}\</title\>
>
   \</head\>
  
`page.title`表示当前页面的标题，该语句表示如果当前页面设置了标题，就显示当前页面的标题，否则显示站点的标题。

`_layouts`中存放的是页面布局文件，对于相同风格的页面可以使用同一布局文件。比如：

> \<\!DOCTYPE html\>
>	
  \<html\>
>
   \{ % include head.html %\}
>			
   \<body\>
>		
   \{ % include header.html %\}
   
>			
   \{\{ content \}\}
>			
   \</body\>
>		
   \</html\>
>	

该布局文件中使用了_includes文件夹中的head.html文件来统一标题风格，`content`为文章的内容部分。

`_posts`中存放的是博客文件，_post文件夹中的文件名必须符合`2015-11-3-file-name.md`这样的格式才会被视为有效的文件，比如：

    ---
    layout: post
    title: 在Github上搭建博客
    date: 2015-10-29 13:21:00
    categories: blog
    excerpt: 在github上搭建静态的博客
    ---

    ## 搭建博客

每篇文章的开头必须有上面的描述信息，`layout`表示使用的是`_layouts`中的哪个布局文件，`title`为该页面的标题，后面的三项可以省略。

`index.html`为博客主页，用来导航到网站的其他页面。

#### 使用现有模板

如果嫌麻烦不想自己去创建站点，或者觉得自己创建的站点不够漂亮，可以在网上搜索一下各种Jekyll theme，然后应用在自己的博客上，[Jekyll Themes](http://jekyllthemes.org)上面提供了很多主题,我这里使用的是[HyG的博客](https://github.com/Gaohaoyang/gaohaoyang.github.io)的主题，搜索到自己满意的主题后，将其下载下来，然后覆盖自己的博客根目录，删掉_posts文件夹内别人的文章，然后修改一下网站的配置信息，注明主题的开发者，做完这些后，上传到Github上就可以了。

#### 撰写博文

博客搭建完了后只需要将文件放在_post文件夹中，同步到远程仓库，就可以通过浏览器访问了。

#### 发布文章

每次将文章添加到_post文件夹中后，通过git将文章从本地同步到Github来实现发布新的文章，比如：

    $git add .
	$git commit -m "new paper"
	$git push origin master

---

## 搭建本地环境(可省略)

为了更方便的在本地预览博客，可以在本地安装Jekyll,安装Jekyll也相当简单，只需要在终端输入

    $gem install Jekyll

就会自动安装Jekyll了，为了和Github上Jekyll环境保持一致，可以键入以下命令

    $gem install github-pages

搭建完本地环境后，可以使用Jekyll按以下步骤创建博客框架

    $cd username.github.io
	$jekyll new .

这时username.github.io文件夹中会自动创建出下列文件和文件夹,包含了所有Jekyll所需要的文件和文件夹。

    _config.yml    整个系统的配置文件
	_includes      放头文件的文件夹，一般会被_layouts文件夹中的文件使用
	_layouts       放布局文件的文件夹，写文章的时候采用里面的布局文件
	_posts         放文章的文件夹	
	_site          jekyll生成的站点文件夹，可以不推送到远程仓库
	index.html    博客系统主页面

用终端进入username.github.io文件夹，输入

    $jekyll serve

就会启动本地的博客服务器，通过浏览器访问`http://localhost:4000`就可以看到jekyll创建博客的主页了。

---

## 参考文章

* [Github Pages](https://pages.github.com/)
* [Github Pages Basics](https://help.github.com/categories/github-pages-basics/)
* [HyG的博客](https://gaohaoyang.github.io)
* [How Jekyll Works](http://jekyllbootstrap.com/lessons/jekyll-introduction.html)
* [Jekyll Themes](http://jekyllthemes.org/)
