---
layout:     post
title:      PDF跨平台解决方案
comments:   true
subtitle:   Reading PDF cross-platform
date:       2018-11-27
author:     Junix
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
- Linux
- PDF
- Academic
---

## Abstract

PDF is generally an academic standard format, and I also use latex to organize my notes. The PDF Reader is very important to me. After wasting a lot of time trying out PDF Readers in the market, I formed my own formula.

## Requests

My requests are not high:
- Cross-platform (Linux & Android)
- Comments and highlights

## the PDF Readers I tried

### PC-end

#### X Change (Windows)

This is the PDF Reader I used in high school (used the win7 stealthy in the classroom, 
this win7 was basically like my personal computer 0.-) is a very good Reader, even if you don't not pay any, 
it provides a lot of Features. 
Although the toolbar is messy, it is very convenient to use after being familiar. 
The fly in the ointment is that Linux is not supported.

#### Evince (Linux)

Evince is simple.
But I got some unendurable bugs when highlighting. 
I don’t know whether it is fixed now.

#### Okular (Linux)

Okular is a very mature **document** reader, with a variety of document formats support, and is quite customizable.
[A blog][2] I ever browsed on the Internet said that Okular was 114M, and evince was only 11M. Indeed, this is also for users. those pdf heavy users might dislike Evince.

The main reason why I choose KDE is that Okualr and [Goldendict][3] are the most convenient pdf reader and dictionary I've ever use.

#### Zathura (Linux)

I know a lot of moguls(大佬) use this, eh...but I've not. So, no use, no more mouths...

#### Master PDF Editor (Linux)

The shortcuts were extremely inconvenient to set up at the time and it didn't have a pleasant cooperation with Goldendict:
the word-taking function is blocked.
Commercial software, and as expensive as Mathematica, anyway, I can't afford it as a poor student.
And there is a very tasteless function: you can modify the pdf in a M$-Word way, but that will generated a pdf with some big watermarks: "This PDF was built by Master PDF Editor". What if you don't like? **Pay** to eliminate the watermarks...

#### Foxit Reader (Linux) 

After knowing that there is praise in zhihu, I tried it. At that time (August 2018), It couldn't be full of screen,
and the shortcuts couldn't be customized. I will never trust zhihu anymore...

### Android

Moon+ is a famous Document Reader on the Android platform.  
It supports a wide range of formats and is equipped with a high responding speed.
It is said that the free version has some features of castration and advertising. 
~~However, there are various cracked versions on the Internet (such as 酷安).~~

Of course, if you don't have financial complications, or you are a "tuhao", please be sure not to make any excuse to support the author of Moon+.

### USB Drive

#### Sumatra PDF 

Imagine you've finished a beamer, only to find your school computer only has Chrome to present your beamer. What a pity!
Installing this on a USB Drive might be your good choice so that your school sucking Windows could help you with a better address...

## Cross-platform synchronization

I am currently using dropbox & Flodersync

### Dropbox

It is said that Google Drive is better, tightly integrated with Google Doc, and has a larger capacity.
But I just searched the Dropbox firstly on the archlinux wiki so installed the official dropbox directly.
If you don't have a dropbox account yet, why not click on my recommended link <https://db.tt/ihSbliC5mF>, so that both of us can get a 500M.

Install Dropbox on Arch:
```
yay -S dropbox
```

Since dropbox's 2GB+500M space is enough for me to sync the books I am reading, I will not continue to toss for the monent.

### Flodersync

Android's official Dropbox, in order to save traffic and space, provides a File list. You have to download the specified file yourself. Not only that, but most of the downloaded files are Read-Only. 
After trying commenting with the Reader, you will find that this file cannot be saved. 
In this case, we can't commit PDF cross-platform annotating happily.

Flodersync (or Dropsync) implements a two-way synchronization function.

## Android dictionary

I currently using the [eudic][4] (commercial software). 
Goldendict also has Android version.
I used eudic firstly, which also supports some formats. So I didn't make a switch.

## Postscript

While playing football, the mobile phone screen had been trodden into terribly crashed by some guy in case I was unconscious. `%>_<%` This is the second time that the screen was broken, so I'm not going to change the screen; 

So, as far as I am concerned, the only purpose of having a mobile phone, is to receive messages from my stupid school who sends important notices only by that stupid tencent QQ??!! 

Um...still, using my dear Arch Linux is always more efficient.

### Reference
1. <https://blog.yuanbin.me/posts/2013-01/2013-01-31_23-07-00/>
2. <https://xuanwo.io/2015/12/23/best-pdf-read-solution/>

[2]: https://blog.csdn.net/u014015972/article/details/50659952
[3]: http://goldendict.org/
[4]: https://www.eudic.net/v4/en/app/download?#mobile

## 摘要

pdf基本是学术标准格式,加上我也用latex整理笔记,pdf阅读器对我来说十分关键。
在浪费了大量时间尝试市面上的阅读器之后，我形成了自己的这一套方案

## 要求

我的要求并不高:

* 跨平台(Linux & Android)
* 批注和高亮


## 尝试的阅读器

### 电脑端

* X change
这是我高中时代使用的阅读器（偷玩教室的win7,这台win7基本上就像我的个人机0.-)
是一款非常优秀的阅读器,即使不付费也提供非常多的功能。

虽然工具栏十分杂乱，但熟悉后使用很方便。
美中不足的是不支持Linux

* Evince
很简洁很小，功能较少。
但当时使用时高亮时bug多多,不知现在有没有修复

* Okular
十分成熟的文档阅读器, 有各种文档格式支持,有相当强的可定制性  
看到网上说Okular有114M，而evince只有11M，确实,这也是看使用者了，pdf重度用户用Evince确实不顺手   
我使用kde的主要原因就是它和goldendict
这两个是我使用最顺手的pdf阅读器和词典

* zathura
很多大佬用这个，没用过，就不多嘴了

* Master PDF Editor
快捷键当时设置起来极不方便。
和goldendict结合使用并不方便,取词功能被屏蔽了。

商业软件，付费贵的要死
有个很鸡肋的功能：可以像word那样修改pdf，但是生成的pdf带水印，付费才能消除水印……

* Foxit Reader
知乎上有好评，我就试了一下。
当时(2018年8月)无法全屏，并且快捷键无法自己定制，差评

### Android

Moon+ 静读天下，安卓平台上首屈一指的阅读器，支持格式众多，速度流畅
据说免费版有些功能阉割和广告。~~但是网上(如酷安)有各种破解版~~

有条件请一定要支持下Moon+的作者

### U盘
* Sumatra PDF

当你做好了beamer, 然而学校电脑却只有chrome能展示你的beamer的时候, 不妨在优盘上装个这个……


## 跨平台同步

目前使用dropbox + Flodersync

### Dropbox

据说google drive更好，和google doc紧密结合,而且容量更大。
但刚好先在archlinux wiki上搜了一下dropbox, 就直接安装官方的dropbox了。

若你还没有dropbox账号，不妨点击我的推荐链接<https://db.tt/ihSbliC5mF>，这样我们都能得到500M

Arch下安装dropbox：
```
yay -S dropbox
```
然后dropbox
2GB+500M的空间正好够我sync正在阅读的书籍，也就没继续折腾了

### Flodersync

安卓端官方的Dropbox,为了节省流量和空间，提供了一个File list，你必须要自己下载指定文件。不仅如此，这个下载下来的文件大多是Read-Only的，用阅读器批注之后，你会发现这个文件无法保存，这样的话，PDF跨平台批注就无从谈起

Flodersync(或者Dropsync)实现了一个双向同步的功能

## Android端的字典

目前使用欧路词典(商用软件)，goldendict也有安卓端，但是先用的欧路，也支持多种格式，就没换了

## 后记

手机屏幕踢球时被别人踩碎了`%>_<%`，这是第二次碎了，不准备换屏了；手机，还是就接收一下讯息吧，嗯，还是用电脑的效率更高
