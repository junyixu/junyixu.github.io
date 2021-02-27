---
layout: post
title: 安装 Bear 冲突的解决方案
subtitle: Install Bear
date: 2021-02-26 22:43:24
author:     Junix
header-img: img/post-bg-2015.jpg
catalog: true
tags:
- Linux
---

# 安装 bear 报错
```sh
$ cd /tmp
$ yay -G aur/bear
$ cd bear
$ makepkg -sir
```
报错
![Install-Bear-Error](/img/install_bear_error.png)

去 aur 看了评论，看起来是与 `interception-tools` 冲突，而其又是改`cap esc` 键必备的包，不能动。

## 为自己安装 bear
我都构建好了 bear, 懒得再构建一遍了，直接
```sh
$ mkdir ~/.local/stow
$ mv pkg/bear/usr ~/.local/stow/bear
$ cd !$
$ cd ..
$ stow bear
```
完工。

不知道这样做是否合理，写篇博客记录下。

## Reference
* [GNU Stow 的使用](https://linux.cn/article-9467-1.html)
* [`$HOME/.local`的用途](https://stackoverflow.com/questions/30274743/what-is-the-purpose-of-home-local)
