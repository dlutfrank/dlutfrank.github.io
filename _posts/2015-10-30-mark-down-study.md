---
layout: post
title: Markdown的使用
date: 2015-10-30 13:21:00
categories: blog
excerpt: Markdown的简单使用
---

* content
{:toc}

Markdown的语法和emacs中org模式的语法很接近，都非常的简单。因为我之前有用过emacs中的org模式，所以编写Markdown文档没有遇到太大的阻碍。

---

## 基本语法

### 插入超链接

超链接的格式如下：

    [链接文字](连接url)
	eg: [小米](http://www.mi.com)
	
例子的效果是这样的:

[小米](http://www.mi.com)

### 插入图片

插入图片的格式也很简单，只需要输入`![alt文字](图片地址)`就能插入图片，用这种方式在Markdown插入图片是没法指定图片的宽和高的，不过可以使用[七牛](http://www.qiniu.com/)做为图床，然后使用七牛提供的[图片接口](http://developer.qiniu.com/docs/v6/api/reference/fop/image/imageview2.html#imageView2-specification)返回指定宽高的图片。

    使用原图:
    ![Alt文字](http://7xntab.com1.z0.glb.clouddn.com/xxx/xxx.JPG)
    限定缩略图最大宽度为200，最大高度为600
    ![Alt文字](http://7xntab.com1.z0.glb.clouddn.com/xxx/xxx.JPG?imageView2/2/w/200/h/600)
	限定缩略图最小宽度为600，最小高度为200
    ![Alt文字](http://7xntab.com1.z0.glb.clouddn.com/xxx/xxx.JPG?imageView2/1/w/600/h/200)

### 插入代码

`缩进4行`就能以代码的形式输出,一定要在`代码前留空一行`。

    #include<stdio.h>
    int main(){
        printf("hello Mark Down\n");
        return 0;
    }

看上去相当赞。

### 文字修饰

需要高亮的文字用两个\`包起来，两个星号`*`和下划线`_`包含的文字会变成斜体，四个星号和下划线包含的文字会变成粗体。

    `高亮文字`
	
    *Hello* _Markdown_
	
	**Hi** __Github__

效果如下:

`高亮文字`

*Hello* _Markdown_

**Hi** __Github__

### 段落引用

要引用某段文字，只需要在段落前加上`>`,如果需要将多个段落连起来一起引用，则在段落之间的空行也需要加上\>标记。

\> I have a dream that one day this nation will rise up, live up to the true meaning of its creed: “We hold these truths to be self-evident; that all men are created equal.”

\>

\> I have a dream that one day on the red hills of Georgia the sons of former slaves and the sons of former slave-owners will be able to sit down together at the table of brotherhood.

效果如下:

> I have a dream that one day this nation will rise up, live up to the true meaning of its creed: “We hold these truths to be self-evident; that all men are created equal.”
>
> I have a dream that one day on the red hills of Georgia the sons of former slaves and the sons of former slave-owners will be able to sit down together at the table of brotherhood.

### 使用列表

Markdown中可以使用无序列表和有序列表，无序列表用星号`*`，加号`+`，减号`-`作为行首标记。有序列表使用`数字`接一个英文句号`.`作为行首标记，标记后面需要空一格。

    * 第一列
	+ 第二列
	- 第三列

    1. 第一列
	2. 第二列
	3. 第三列
    
效果如下：
	
* 第一列
+ 第二列
- 第三列

1. 第一列
2. 第二列
3. 第三列

### 字符转义

有的时候我们不希望对特殊字符进行转义，只需要在特殊字符前加一个`反斜杠\`就可以了,比如输入\\\`就可以禁止\`转义。

---

## emacs中编写Markdown

通过emacs的markdown模式能非常方便的编辑Markdown格式的文件，首先需要下载[markdown-mode.el](http://jblevins.org/projects/markdown-mode/markdown-mode.el)，然后将markdown-mode.el文件放入emacs的加载路径下，比如*~/.emacs.d/*文件夹中，最后在`.emacs`中加入以下代码，使得emacs在打开`.md`,`.markdown`,`.text`文件的时候自动使用markdown模式。

    (autoload 'markdown-mode "markdown-mode"
    "Major mode for editing Markdown files" t)
    (add-to-list 'auto-mode-alist '("\\.text\\'" . markdown-mode))
    (add-to-list 'auto-mode-alist '("\\.markdown\\'" . markdown-mode))
    (add-to-list 'auto-mode-alist '("\\.md\\'" . markdown-mode))

### 快捷键

|快捷键     |作用     |Markdown符号 |
|----------|:------:|:------:|
|C-c C-t 数字| 标题| \# \#|
|C-c C-s e |斜体|\* \*|
|C-c C-s s |粗体|\*\* \*\*|
|C-c C-s b|引用|\>|
|C-c C-i i|插入图片|!\[\]\(\)|
|C-c C-a l|插入链接|\[\]\(\)|
|C-c -|插入水平线|------|

有些快捷键使用起来还不如直接使用Markdown符号方便，比如引用快捷键。我经常使用到的快捷键只有插入标题，插入图片，插入链接和插入水平线。

---

## 参考文献

* [Emacs Markdown Mode](http://jblevins.org/projects/markdown-mode/)
