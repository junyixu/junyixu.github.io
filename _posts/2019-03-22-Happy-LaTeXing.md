---
layout:     post
title:      在 ArchLinux 上愉快地 LaTeXing
subtitle:   Happy LaTeXing
date:       2019-02-22
author:     Junix
header-img: img/post-bg-unix-linux.jpg
catalog: true
tags:
- Linux
- vim
- latex
- 知识管理
---

## 摘要
这是一篇我在 ArchLinux 下 ~~clone 别人的模版后~~ 用 vim 流畅地 LaTeXing 的小记

![效果图](/img/latexing.gif)

## 这或许是个系列

灵感来自于 萌狼姐姐的 [知识管理ABC](https://blog.yoitsu.moe/life/knowledge_manage_0.html)  
我的知识管理体系太乱了，记笔记或者 todolist 大致有这么几个地方

#### 纸质:
* [ ] 存放 4A纸的文件夹 和 使用彩色标签标记的活页笔记本
#### 电子:
* [ ] vimwiki 
* [ ] 滴答清单
* [ ] anki
* [ ] 印象笔记: 用来网页剪藏
* [ ] simplenote
* [ ] pocket, Liner 以及 firefox 的书签
* [ ] LaTeX: 主要用来整理公式多的笔记

## 用料
* texlive
* vim 及其插件
	* aperezdc/vim-template
	* lervag/vimtex
	* xuhdev/vim-latex-live-preview
	* SirVer/ultisnips 和 honza/vim-snippets
* [mathpix](https://mathpix.com/)

### 安装 texlive
#### 方法一
查阅 `texlive-zh-cn`
使用 Unix installer 安装: 可使用国内大学的开源镜像站，wget 下载 install-tl，执行
install-tl 脚本。

#### 方法二
使用源上的 texlive

##### 优点
* 统一管理
* 方便快捷: 对照着 ArchLinux Wiki 直接用 pacman 安装所需的包即可，参考
  <https://wiki.archlinux.org/index.php/TeX_Live>

##### 缺点
无法使用 `texdoc`命令 查看文档  (~~然而我只是 tex 小白，看完 lshort后，~~
~~会用几个宏包， 使用个模版, 熟练地编辑数学公式已经很 happy 啦~~)

不过可以查看在线文档嘛

### vim 插件
#### [vim-template](https://github.com/aperezdc/vim-template)
安装后就可以用了  
如用 vim 直接创建一个 .c 结尾的文件就会出现 c文件的模版

当然你可以创建自己的模版文件  
则在vim配置文件中写入

```
let g:templates_directory = '/home/pylego/.vim/templates'
```
文件的命名模式是"=template=<pattern>"  
如我的 [templates 文件夹](https://github.com/junyixu/dotfiles/tree/master/vim/templates)


#### [vimtex](https://github.com/lervag/vimtex)
很多人使用 vim-latex 
我个人并不推荐 vim-latex 而是推荐使用 vimtex 搭配 Ultisnips

vimtex 的常见快捷键
* 普通模式下
	- 使用`dsc`/`dse`/`ds$`/`dsd` 删除周围的命令(command)，环境(environment)，计数器(delimiter)
	- 使用`csc`/`cse`/`cs$`/`csd` 修改周围的命令(command)，环境(environment)，计数器(delimiter)
	- 使用 `tsc`/`tse`使命令(command)或者环境(environment)在加`*`和不加`*`之间互相切换
	-  使用`tsd`/`tsD`使括号在`()` 和 `\left(\right)` 两状态互相切换
	- 使用 `<F7>` 插入新的命令


* 插入模式下
	* 使用 `]]` 关闭 当前环境或计数器, 如: 在末尾添加`end{your environment}`

#### [Ultisnip](https://github.com/SirVer/ultisnips)
这只是个代码块引擎

你还需要代码块集合
前人栽树后人乘凉，我们可以下载别人写好的代码块集合 如 [honza/vim-snippets](https://github.com/honza/vim-snippets)
当然，我们可以在 `~/.vim/UltiSnips/` 目录下创建我们自己的代码块集合作为补充
如不嫌弃，可以看看[我的UltiSnips目录](https://github.com/junyixu/dotfiles/tree/master/vim)

#### [vim-latex-live-preview](https://github.com/xuhdev/vim-latex-live-preview)
这个插件起到了即时预览的作用
配置好你的 pdf 浏览器 比如这里我用 okular
```
let g:livepreview_previewer = 'okular'
```
使用 vim 编辑 .tex时 使用`:LLPStartPreview`即可打开预览

#### YCM
由于我同时使用 YCM 和 Ultisnips 造成了 tab 键冲突
，参考这篇文章解决了 YCM 和 Ultisnips 使用 tab 键的冲突
	  <https://stackoverflow.com/questions/14896327/ultisnips-and-youcompleteme>
如果您有更好的办法恳请您不吝赐教

### [mathpix](https://mathpix.com/)
原本 archlinuxcn 源上是有的  `/(ㄒoㄒ)/~~)`  
后来由于没有协议，认为不能分发  
无奈，从 aur 上下载安装吧
	  
## 参考
<http://mednoter.com/UltiSnips.html>
<https://segmentfault.com/a/1190000006036434>
