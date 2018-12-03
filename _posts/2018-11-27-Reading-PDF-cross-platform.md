---
layout:     post
title:      PDF跨平台解决方案
comments:   true
subtitle:   Reading PDF cross-platform
date:       2018-11-27
author:     Junix
header-img: img/post-bg-coffee.jpg
catalog: true
tags:
    - Linux
    - PDF
    - Academic
---

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
虽然工具栏十分杂乱，但熟悉后使用很方便
美中不足的是不支持Linux

* Evince
很简洁很小，功能较少
但当时使用时高亮时bug多多,不知现在有没有修复

* Okular
十分成熟的文档阅读器, 有各种文档格式支持,有相当强的可定制性  
看到网上说Okular有114M，而evince只有11M，确实,这也是看使用者了，pdf重度用户用Evince确实不顺手   
我使用kde的主要原因就是它和goldendict
这两个是我使用最顺手的pdf阅读器和词典

* zathura
很多大佬用这个，没用过，就不多嘴了

* Master PDF Editor
快捷键当时设置起来极不方便
和goldendict结合使用并不方便,取词功能被屏蔽了

商业软件，付费贵的要死
有个很鸡肋的功能：可以像word那样修改pdf，但是生成的pdf带水印，付费才能消除水印……

* Foxit Reader
知乎上有好评，我就试了一下
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
