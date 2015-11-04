---
layout: post
title: Markdown的使用
date: 2015-10-30 13:21:00
categories: blog
excerpt: Markdown的简单使用
---

* content
{:toc}

Markdown的语法和emacs中org模式的语法很接近，都非常的简单。因为我之前有用过emacs中的org模式，所以感觉熟悉Markdown还是比较容易。

---

## 基本语法

### 插入超链接

超链接的格式如下：

    [链接文字](连接url)
	eg: [小米](http://www.mi.com)
	
例子的效果是这样的:

[小米](http://www.mi.com)

### 插入图片

插入图片的格式也很简单，只需要输入`![alt文字](图片地址)`就能插入图片，用这种方式在Markdown插入图片是没法指定图片的宽和高的，不过可以使用[七牛](http://www.qiniu.com/)做为图床，然后使用七牛提供的[图片接口](http://developer.qiniu.com/docs/v6/api/reference/fop/image/imageview2.html)返回指定宽高的图片。

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

### 高亮文字

需要高亮的文字用两个\`包起来，eg:\`高亮文字\`,效果为是`高亮文字`。

### 字符转义

有的时候我们不希望对特殊字符进行转义，只需要在特殊字符前加一个`反斜杠\`就可以了,比如输入\\\`就可以禁止\`转义。

---

## emacs中编写Markdown

---

## 用Markdown写博客

---

## 总结
