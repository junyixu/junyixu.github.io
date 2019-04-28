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
这是一篇我在
[ArchLinux](https://blog.yoitsu.moe/life/archlinux_cn_community_unoffical_newbie_guide.html)
下 ~~clone 别人的模版后~~ 用 vim 流畅地整理笔记的小记。自从用了 LaTeX （雷太赫） 之后再也不想回 M$ Word 了：
* [LaTeX 是内容与样式分离的](https://liam.page/2019/03/18/separation-of-content-and-presentation/)
* 再也不要打开 Word 等数秒钟啦，只要在终端输入 gvim(或vim或nvim) *.tex 后瞬间 template 就位，
  甚至光标也处于对应位置，你要做的只是所思即所得
* 公式体验好，Ultisnips 加成，平均速度几乎可以和手写一样

![效果图](/img/latex3.gif)
笔记模版用的是 [ElegantNote](https://github.com/ElegantLaTeX/ElegantNote)

## 或许是个系列

灵感来自于 萌狼姐姐的 [知识管理ABC](https://blog.yoitsu.moe/life/knowledge_manage_0.html)    
我的知识管理体系太乱了，记笔记或者 todolist 大致有这么几个地方

#### 纸质:
* [ ] 存放 A4 纸的文件夹 和 使用彩色标签标记的活页笔记本

#### 电子:
* [ ] 滴答清单
* [ ] [Goldendict](https://github.com/Dictionaryphile/GoldenDict_zh_manual)
* [ ] [Anki](https://zhuanlan.zhihu.com/p/31100580)
* [ ] OneNote: 只是用来网页剪藏`~~~~(>_<)~~~~)`若你有什么网页剪藏的好软件请告诉我
* [ ] [Simplenote](https://app.simplenote.com/)
* [ ] VimWiki 
* [ ] inoreader
* [ ] pocket, Liner(火狐插件) 以及火狐书签
* [X] LaTeX: 主要用来整理公式多的笔记

为什么要用 LaTeX 整理笔记呢，当然是因为没有惠狐姐姐那么清秀的字迹啦。  
时间长了我自己都不认识我当时在写什么了……
![字迹](/img/ugly.jpg)

[惠狐姐姐的 Wacom Bamboo Slate](https://blog.megumifox.com/public/2018/12/07/wacom-bamboo-slate-review/)…
~~Hmmm, 考完试忘写了（逃~~

![评论](/img/latex2.png)

## 用料
* texlive
* vim 及其插件
	* aperezdc/vim-template
	* lervag/vimtex
	* SirVer/ultisnips 和 honza/vim-snippets
* [mathpix](https://mathpix.com/)

### 在 Linux 上安装 texlive

#### [方法一](https://stone-zeng.github.io/2018-05-13-install-texlive-ubuntu/)
查阅 `texlive-zh-cn`
使用 Unix installer 安装: 可使用国内大学的开源镜像站，wget 下载 install-tl，执行
install-tl 脚本。

#### 方法二
使用源上的 texlive  
(**非 Arch Linux 用户**请使用[方法一](https://stone-zeng.github.io/2018-05-13-install-texlive-ubuntu/)安装，以使用最新版本)

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
文件的命名模式是"`=template=<pattern>`"  
如:我的 [templates](https://github.com/junyixu/dotfiles/tree/master/vim/templates/)


#### [Vimtex](https://github.com/lervag/vimtex)
我曾 google "vim latex"，一堆使用 vim-latex 的文章。 我个人并不推荐。  
而是主张使用 vimtex README 上所推荐的：**vimtex 搭配 Ultisnips**.

Vimtex 轻量且功能强大，这里只列举几个 to make it work(以后有时间再补充)
* 普通模式下
	- 使用`dsc`/`dse`/`ds$`/`dsd` 删除周围的命令(command)，环境(environment)，计数器(delimiter)
	- 使用`csc`/`cse`/`cs$`/`csd` 修改周围的命令(command)，环境(environment)，计数器(delimiter)
	- 使用 `tsc`/`tse`使命令(command)或者环境(environment)在加`*`和不加`*`之间互相切换
	-  使用`tsd`/`tsD`使括号在`()` 和 `\left(\right)` 两状态互相切换
	- 使用 `<F7>` 插入新的命令


* 插入模式下
	* 使用 `]]` 关闭 当前环境或计数器, 如: 在末尾添加`end{your environment}`
	 
* 即时预览
 
配置好 vimtex 后([我的插件配置](https://github.com/junyixu/dotfiles/blob/master/vim/plugs.vim))  
使用 vim 编辑 .tex时 输入`:VimtexCompile`即可打开预览（当`:w`时会自动刷新）。  
若嫌此命令太长可以 map 一下。

* 符号替换
 
替代文本里夹杂的 LaTeX 代码为相对应的 Unicode，使 *.tex 更易读。等到写个一个多
月的 LaTeX，练熟 LaTex 后，你可能根本不需要再用即时预览了，这个功能会很有用，真正做到所思即
所得。

若你需要更好的效果可以尝试插件[KeitaNakamura/tex-conceal.vim](https://github.com/KeitaNakamura/tex-conceal.vim)

#### [Ultisnip](https://github.com/SirVer/ultisnips)
这**只**是个代码块引擎  
你还需要代码块合集

前人栽树后人乘凉，我们可以下载别人写好的代码块合集 如
[honza/vim-snippets](https://github.com/honza/vim-snippets)(几乎囊括了所有语言)  
当然，也可以在 `~/.vim/UltiSnips/` 目录下创建我们自己的代码块合集作为补充。  
如不嫌弃，可以看看[我的UltiSnips目录](https://github.com/junyixu/dotfiles/blob/master/vim/UltiSnips/tex.snippets)

之后我们就可以愉快地使用 snips 啦。  
举个例子：输入`b<tab>`
补全
再按
`tab` 跳转到下一个


#### You Complete Me

我参考[这篇文章](https://stackoverflow.com/questions/14896327/ultisnips-and-youcompleteme)
解决了同时使用 YCM 和 Ultisnips 造成的 tab 键冲突

如果您有更好的办法恳请您不吝赐教

### [mathpix](https://mathpix.com/)
原本 archlinuxcn 源上是有 mathpix 的  `/(ㄒoㄒ)/~~)`  
后来由于没有协议，认为不能分发  
无奈，从 aur 上下载安装吧

其实有了 snips 不需要 mathpix 了，但是写论文时可以从已有的电子书上直接抄公式也是
懒癌症患者的乐事啊。

以及，若突然忘记某个公式怎么用 LaTeX 写了，可以点[这个网站](https://webdemo.myscript.com/views/math/index.html)来手写输入
	  
## 参考
<http://mednoter.com/UltiSnips.html>  
<https://segmentfault.com/a/1190000006036434>


## 后记
这个世界啊...在我写好这篇博客的数天后，偶然发现一比利时小哥的一篇用 vim 来 LaTeXing 的博
文，
而且这位几乎把 代码块 用到了炉火纯青的境界，我这篇相形见绌了。
这里推荐下：
<https://castel.dev/post/lecture-notes-1/>

（后来我基本上把他的代码块全部抄袭了，小哥没给出他的配置，有需要的初学者可以参
考我的点文件）
