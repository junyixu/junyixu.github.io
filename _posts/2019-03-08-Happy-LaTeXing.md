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

这是一篇我在
ArchLinux
下用 vim 愉快地整理笔记的小记。

## 写在前面

### 关于 latex 本身
在 Unix like 上用 latex 会更加舒适。

latex 很适合“输出”，比如说写实验报告
（手动滑稽）
```
cp 实验报告1 实验报告2
```
以及写论文，写书（其实 TeX 被发明就是用来写书的）, 不适合用来“输入”-- 把知识理解吸收并印到**脑子**里你只需要纸、笔和**大脑**．(长期记忆可能需要 anki, 不过这是题外话了) 我也只是用 latex 整理笔记（归档）．或者你要电子化，完全可以用类似于 比如说 [惠狐姐姐的
WacomBambooSlate](https://blog.megumifox.com/public/2018/12/07/wacom-bamboo-slate-review/) 或者 OneNote

## 一些说服你使用 LaTeX （雷太赫） 的理由
* 公式体验好，Ultisnips 加成，平均速度几乎可以和手写一样
* Pandoc 可以愉快地把 .tex 转换为多种格式
* [用雷太赫可以解决大学学业生涯上一个非常根本的需求（maybe）](http://www.kylen314.com/archives/7245)

![效果图](/img/latex3.gif)
笔记模版用的是 [elegantnote](https://github.com/ElegantLaTeX/ElegantNote)

这里补充说明下
* vim-template: 用 vim 打开任意空文件就会根据你的后缀（如.cpp) 出现相应的模版
* LaTeX 模版：以.cls 结尾的文本文件，比如，**ArchLinux**官方包的安装路径是在`/usr/share/texmf-dist/tex/latex/`目录下；使用时只要将.cls 之前的**该文本文件的名字**放在 documentclass 的花括号里面就行了。vimtex 对 vim 本身的 `gf` 命令做了修改，把光标放在花括号里面的 cls 名字上，按 `gf` 就可以跳转进该文件．


## 用料
* texlive
* vim 及它的小伙伴们
	* aperezdc/vim-template
	* lervag/vimtex
	* SirVer/ultisnips 和 honza/vim-snippets
    * fzf 和 ripgrep
    * ycm
    * junegunn/vim-easy-align
    * tagbar 用于显示大纲
    * textobj 全家桶
* ~~mathpix~~

### 在 Linux 上安装 texlive

#### [方法一](https://stone-zeng.github.io/2018-05-13-install-texlive-ubuntu/)
查阅 `texlive-zh-cn`
使用 Unix installer 安装：可使用国内高校的开源镜像站，wget/curl 下载 install-tl，执行
install-tl 脚本。
装完后别忘了装 archlinuxcn/texlive-dummy 之类的包．

（若只装中英文大约占用 4G 多的硬盘空间，3G 都是文档）

#### 方法二
使用源上的 texlive
(**非 Arch Linux 用户**请使用[方法一](https://stone-zeng.github.io/2018-05-13-install-texlive-ubuntu/) 安装，以使用最新版本）

（大约 1.5G，明明比 office 套件小多了好吗）

##### 优点
* 统一管理
* 方便快捷：对照着 ArchLinux Wiki 直接用 pacman 安装所需的包即可，参考
  <https://wiki.archlinux.org/index.php/TeX_Live>

##### 缺点
无法使用 `texdoc`命令 查看文档  (~~然而我只是 tex 小白，看完 lshort 后，~~
~~会用几个宏包， 使用个模版，熟练地编辑数学公式已经很 happy 啦~~)
不过可以查看在线文档嘛 （网差还是用方法一吧，文档真的很重要，**latex 很多东西不是记的，而是查的**)

### vim 的一些配置


#### [vim-template](https://github.com/aperezdc/vim-template)
安装后就可以用了
如用 vim 直接创建一个 .c 结尾的文件就会出现 c 文件的模版

当然你可以创建自己的模版文件
在 vim 配置文件中写入

```
let g:templates_directory = '$HOME/.vim/templates'
```
文件的命名模式是"`=template=<pattern>`"
如：我的 [templates](https://github.com/junyixu/dotfiles/tree/master/vim/templates/)


#### [Vimtex](https://github.com/lervag/vimtex)
我曾 google "vim latex"，一堆使用 vim-latex 的文章。 我个人并不推荐。
而是主张使用 vimtex README 上所推荐的：**vimtex 搭配 Ultisnips**.

vimtex 自定义了几个文本对象，比如 `cae` 去 change around environment, `=ae` 去对齐整个环境

* 一些文本对象
	- 使用`dsc`/`dse`/`ds$`/`dsd` 删除周围的命令 (command)，环境 (environment)，计数器 (delimiter)
	- 使用`csc`/`cse`/`cs$`/`csd` 修改周围的命令 (command)，环境 (environment)，计数器 (delimiter)
	- 使用 `tsc`/`tse`使命令 (command) 或者环境 (environment) 在加`*`和不加`*`之间互相切换
	-  使用`tsd`/`tsD`使括号在`()` 和 `\left(\right)` 两状态互相切换


* 即时编译
此功能其实是调用 latexmk 之类的一些自动编译脚本，请查看 latexmk 和 vimtex 的文档使用 vim 编辑 .tex 时 输入`:VimtexCompile`即可打开预览（当`:w`时会自动刷新）。
若嫌此命令太长可以 map 一下。

我常用的几个快捷键：

* `<leader>ll` 编译
* `<leader>le` 打开 quickfix 快速跳转到出错的地方（其实我很少用，配合 ale，基本不会有什么错）
* `<leader>lv` 正向查找

反向查找 请 :help vimtex 自己阅读文档，vimtex 支持多种文档阅读器

* 符号替换
替代文本里夹杂的 LaTeX 代码为相对应的 Unicode，使 *.tex 更易读。等到你写了近一个
月的 LaTeX，练熟 LaTex 后，可能根本不需要再用即时预览了。这时，此功能会很有用，真正做到所思即所得。
【注】: 确保你的字体支持此功能，比如 windows 的 Courier_New 就会把符号映射成豆腐块。
若你需要更好的效果可以尝试插件 [PietroPate/vim-tex-conceal](https://github.com/PietroPate/vim-tex-conceal)

#### [Ultisnip](https://github.com/SirVer/ultisnips)

推荐 <https://castel.dev/post/lecture-notes-1/> 的 snips
（后来我基本上~~抄袭~~学习他的代码块

#### You Complete Me
vimtex 支持很多补全插件， 我需要用 ycm 写其他语言，就用 ycm 了．详情请 `:help vimtex`

我参考[这篇文章](https://stackoverflow.com/questions/14896327/ultisnips-and-youcompleteme)
解决了同时使用 YCM 和 Ultisnips 造成的 tab 键冲突

如果您有更好的办法恳请您不吝赐教

### [mathpix](https://mathpix.com/)
原本 archlinuxcn 源上是有 mathpix 的  `/(ㄒoㄒ)/~~)`
后来由于没有协议，认为不能分发
无奈，从 aur 上下载安装吧

其实有了 snips 不需要 mathpix 了，但是写论文时从已有的电子书上直接抄公式也是
懒癌患者的乐事啊。

若突然忘记某个公式怎么用 LaTeX 写了，可以点[这个网站](https://webdemo.myscript.com/views/math/index.html) 来手写输入

## 宏包推荐
* physics 写矩阵特舒服
* siunitx 用于写单位
