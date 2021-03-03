---
layout: post
title: 数模美赛排版遇到的问题
subtitle: MCM-Problems
date: 2021-02-13 18:55:20
author:     Killua
header-img: img/post-bg-map.jpg
tags:
- latex
- cooperation
---

## 小的注意点

1. 句号逗号: 前面没有空格，后面有空格
2. 空格`(`内容`a)`空格，即：括号左右两边要加空格
3. 若不是换行就不要自己插入回车不然会有 `^M`
4. 表示百分号要在前面加 `\%`
5. 用`~`表示空格： `Fig.~ref`

## 同步
我们用坚果云同步，然后我把 `fig` 文件夹链接到我的latex目录, 把 `main.pdf` 链接回 `latex.out`

但是c题的数据集特别大，我们的坚果云免费流量就用完了。如果我在放假前帮队友装上 syncthing 的话可能就不存在这个问题了。

## 表格和图片的引用

![美赛图片引用](/img/美赛latex图片ref.gif)
* 在用 word 写作的时候，队友直接写 as shown in `图片/表格` 的`文件名`就行了，可以要求队友给该`文件名`加高亮以提醒自己在这里插图片和表格(以“立体图”举例)。
* `\usepackage{showkeys}` 显示标签名, 在最终版删掉即可

## `-` 的用法
* `-`断词
* `--` 破折号
* `---` 长破折号
* `\-` 你想让latex断词并换行的地方(大部分情况不要加，latex会自己断词)
* `-\\` 强制断词并换行

## `\paragraph{topic}` 和 `\subparagraph{topic}`
以前没有注意这个命令，美赛的时候发现表达一个主题在不适合用`\subsubsection{}`的时候用这个很好。

## 使用参考文献
用 word 写作的同学把半页多的 word 版参考文献发给我的时候我是崩溃的，这样不仅参考文献的格式不好调整(书籍和文章的格式就是不一样的)，而且我复制粘贴的时候非常容易出错。

正确的做法应该是把 bib 文件(在谷歌学术等网站上复制粘贴即可) 发给我，这样就不用关心参考文献的格式了。这些事情要事先协商好(我正在参考文献的时候已经天亮了, 便暴力地复制粘贴用vim的宏录制解决了)。

## latex 中引用参考文献的正确方法

我使用 zotero + better bibtex, 最开始使用的时候只需要点`导出文献库`, 选中 `Keep updated`, 导出到 `~/texmf/bibtex/bib/myLibrary.bib`, 以后只需要向 zotero 添加文献，better bibtex 就能自动更新 bib 文件

编辑 `main.tex` 的时候只需要在末尾添加 `\bibliography{myLibrary}` (是的没错， 如果你导出到`~/texmf/bibtex/bib/myLibrary.bib`, 就不需要在前面加路径；另，`myLibrary` 是我随便起的名字)
就能 在需要的地方 `\cite{cite_key}`，并且这个 cite key 是可以用 ycm 糢糊补全的，就算不安装任何补全插件，使用 `^X^O` 也可以用 `omni` 以正则表达式的形式补全

vim 的 `omni` 可以用在三个地方
* 文档类
* 宏包
* bibsytle

注：`\bibliography{}` 里面不支持用`~`表示家目录，即：如果用绝对路径需要写`/home/YOURUSERNAME`

## 我的小发明：中英对译

```latex
\usepackage{parallel}
\usepackage{tagging}
% \usetag{Chinese}
\newcommand{\translate}[2]{
	\iftagged{Chinese}{
		\ParallelLText{
		{ #2}
	}
	\ParallelRText{
		{ #1}
		} \ParallelPar
	}
	{ #1}
}
```
使用方式
```
\begin{Parallel}[c]{0.52\textwidth}{0.43\textwidth}
\translate{中文句子}{英文句子}
\end{Parallel}
```
就可以中英并排排版了，注释 ` \usetag{Chinese}` 以恢复全英文排版

你以为这就完了？

还可以这样玩：  
先写完中文，然后用 vim 的 Ultisnip 插件，第一个大括号里面用 VISUAL, 第二个大括号里面返回翻译(可以用各个大厂的翻译API, 我偏爱百度的翻译)。最后再对照中文进行细调。

## 打包项目给别人
在项目当前目录的`.latexmkrc`中写入：
```
$pdf_mode = 5;
$pdflatex = "pdflatex -file-line-error -halt-on-error -interaction=nonstopmode -shell-escape -synctex=1 %O %S";
$xelatex = "xelatex -file-line-error -halt-on-error -interaction=nonstopmode -shell-escape -no-pdf -synctex=1 %O %S";
$xdvipdfmx = "xdvipdfmx -E -o %D %O %S";

$bibtex_use = 1.5;
$clean_ext = "hd nav snm synctex.gz xdv";
@default_files = ('main.tex');
```
让别人在终端运行 `latexmk` 就能编译出 pdf 了(需要把`myLibrary.bib`也放入当前目录)

## Reference
* <https://github.com/skywind3000/translator>
