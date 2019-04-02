---
layout:     post
title:      在 ArchLinux 上愉快地 LaTeXing
subtitle:   Happy LaTeXing
date:       2019-03-08
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
这是一篇我在 [ArchLinux](https://blog.yoitsu.moe/arch-linux/installing_arch_linux_for_complete_newbies.html) 下 ~~clone 别人的模版后~~ 用 vim 流畅地记笔记的
小记。自从用了 latex 之后再也不想回 word 了：
* [LaTeX 是内容与样式分离的](https://liam.page/2019/03/18/separation-of-content-and-presentation/)
* 再也不要打开 word 等数秒钟啦，只要在终端输入 gvim(或vim或nvim) *.tex 后瞬间 template 就位，
  甚至光标也处于对应位置，你要做的只是所思即所得
* 公式体验好，Ultisnips 加成，平均速度几乎可以和手写一样

![效果图](/img/latex3.gif)

## 这或许是个系列

灵感来自于 萌狼姐姐的 [知识管理ABC](https://blog.yoitsu.moe/life/knowledge_manage_0.html)    
去年，[惠狐姐姐买了Wacom Bamboo Slate](https://blog.megumifox.com/public/2018/12/07/wacom-bamboo-slate-review/)…
~~Hmmm, 考完试忘写了（逃~~

![评论](/img/latex2.png)

我的知识管理体系太乱了，记笔记或者 todolist 大致有这么几个地方

#### 纸质:
* [ ] 存放 A4 纸的文件夹 和 使用彩色标签标记的活页笔记本

#### 电子:
* [ ] vimwiki 
* [ ] 滴答清单
* [ ] anki
* [ ] 印象笔记: 用来网页剪藏
* [ ] simplenote
* [ ] inoreader
* [ ] pocket, Liner(火狐插件) 以及火狐书签
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
(非 Arch 用户请使用方法一安装，以使用最新版本)

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
在vim配置文件中写入

```
let g:templates_directory = '$HOME/.vim/templates'
```
文件的命名模式是"=template=<pattern>"  
如:我的 

[templates](https://github.com/junyixu/dotfiles/tree/master/vim/templates/)


#### [vimtex](https://github.com/lervag/vimtex)
我曾 google "vim latex"，一堆使用 vim-latex 的文章。 我个人并不推荐。  
而是主张使用 vimtex README 上所推荐的：**vimtex 搭配 Ultisnips**.


vimtex 轻量且功能强大，这里只列举几个快捷键(以后有时间再补充)
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
你还需要代码块合集

前人栽树后人乘凉，我们可以下载别人写好的代码块合集 如 [honza/vim-snippets](https://github.com/honza/vim-snippets)
当然，也可以在 `~/.vim/UltiSnips/` 目录下创建我们自己的代码块合集作为补充。  
如不嫌弃，可以看看[我的UltiSnips目录](https://github.com/junyixu/dotfiles/blob/master/vim/UltiSnips/tex.snippets)

之后我们就可以愉快地输入`b<tab>`
补全
再按
`tab` 或者`<ctrl-J>`跳转到下一个

#### [vim-latex-live-preview](https://github.com/xuhdev/vim-latex-live-preview)
这个插件起到了即时预览的作用。
配置好你的 pdf 阅读器 比如这里我用 okular
```
let g:livepreview_previewer = 'okular'
```
使用 vim 编辑 .tex时 输入`:LLPStartPreview`即可打开预览  
~~然而，vim 用户真的会打这么长的命令吗，当然是 map 一下啦~~

查看`vimtex`的手册，它似乎自带预览命令，不过我没理解怎么使用。

#### You Complete Me

我参考[这篇文章](https://stackoverflow.com/questions/14896327/ultisnips-and-youcompleteme)
解决了同时使用 YCM 和 Ultisnips 造成的 tab 键冲突

如果您有更好的办法恳请您不吝赐教

### [mathpix](https://mathpix.com/)
原本 archlinuxcn 源上是有 mathpix 的  `/(ㄒoㄒ)/~~)`  
后来由于没有协议，认为不能分发  
无奈，从 aur 上下载安装吧
	  
## 参考
<http://mednoter.com/UltiSnips.html>  
<https://segmentfault.com/a/1190000006036434>


## 后记
这个世界啊...在我写好这篇博客的数天后，偶然发现国外一篇用 vim 来 LaTeXing 的博
文，
而且这位几乎把 代码块 用到了炉火纯青的境界，我这篇相形见绌了。
这里推荐下：
<https://castel.dev/post/lecture-notes-1/>
