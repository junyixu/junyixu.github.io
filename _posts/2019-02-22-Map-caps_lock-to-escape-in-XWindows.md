---
layout:     post
title:      使用 xmodmap 交换 Esc 和 Caps Lock 按键
subtitle:   Map-caps_lock-to-escape-in-XWindows
date:       2019-02-22
author:     Junix
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
- Linux
- vim
- Xorg
- XWindows
---
### 适用环境和人群
测试环境是 ArchLinux 和 Xorg 

Ctrl 键我是用小指和手掌相连的那块软肉按的，但是 Esc 键实在太远……

快速地进入普通模式 对 vim user 来说十分重要；当然，方法不唯一，我知道有人使用
<C-[> 去实现 `Escape`，但对我而言，`Caps Lock`是最不常用的按键并且最好按的键
。

以及 oh-my-zsh + tmux + vim及其各种插件 大大提升了我在命令行下的效率。什么？？？你居然还不知道 `zsh` 和 `tmux` 为
何物？Hmmm, 这里推荐一下[程序员内功篇](https://xiaozhou.net/learn-the-command-line-preface-2017-05-12.html)
### 方案 A
在查看系统按键映射可以在终端下输入：`xmodmap -pke`

要交换 Esc 和 Caps Lock 按键，输入命令：```xmodmap -```，然后再输入：

```
remove Lock = Caps_Lock
keysym Caps_Lock = Escape
keysym Escape = Caps_Lock
add Lock = Caps_Lock
```

这里解释一下：
* 第一行清除`CapsLock`的 Modifier 映射 （或者你用 `clear Lock` 替代 `remove Lock
  = Caps_Lock` 效果是一样的)
* 第二行和第三行交换`Escape`和`Caps_Lock`的映射
* 最后一行加上对`CapsLock`的 Modifier 映射。

这样`Esc`就完成大写锁定的功能，而```CapsLock```则完成```Esc```的功能。  
大功告成！！！接下来将上述代码写入配置文件```$HOME/.Xmodmap```里。


即: `vim ~/.Xmodmap` 写入

```
! 方案 A
remove Lock = Caps_Lock
keysym Caps_Lock = Escape
keysym Escape = Caps_Lock
add Lock = Caps_Lock
```
保存并退出  
然后执行
```
xmodmap ~/.Xmodmap
```
即可。

若你不需要挂起或休眠，**看到这里就可以了**。

【注】 startx 会在启动时按 /etc/X11/xinit/xinitrc 的要求去找 ~/.Xmodmap 这个文件
。  
详情请参考：[ArchLinuxWiki](https://wiki.archlinux.org/index.php/Xmodmap)


这个方法**挂起**或**休眠**后再开启电脑时就会失效，此时，若你去尝试去`xmodmap ~/.Xmodmap`会报错,
大致像这样子：
* 第一个错误是

```
xmodmap:  /home/junyi/.Xmodmap:16:  bad keysym in remove modifier list
'Caps_Lock', no corresponding keycodes
xmodmap:  1 error encountered, aborting.
```
* 第二个错误说 `Caps_Lock` 与 `Escape` 找不到之类

### 方案 A pro

通过
```
xmodmap -pke > ~/.Xmodmap
```
你会得到一张键位映射表。  

你也许会想把`Escape` 和 `Caps_Lock` 对应的数字互换  
比如在我的机器上，这两个键分别对应 9 和 66,  
(**注意** `Escape` 和 `Caps_Lock` 具体的 `keycode` 究竟是不是 9 和 66 可能会根据你的键盘而有所不同。)  
这样做是不行的，因为没有消除 `Lock` 键：按 `Caps_Lock` 键后同时表现 `Escape`和“大小写锁定”

少年，请找到属于你的 `keycode`，然后执行
```
rm ~/.Xmodmap  #删除刚才的表
vim ~/.Xmodmap
```
写入下面这些代码

```
! 方案 C
remove Lock = Caps_Lock
keycode  9 = Caps_Lock NoSymbol Caps_Lock
keycode  66 = Escape NoSymbol Escape
add Lock = Caps_Lock
```
保存并退出(**请把9 和 66 换成你的数字**)

最后执行  
`xmodmap ~/.Xmodmap`


好了，再次**挂起**或**休眠**试试吧，好了，祝贺你，愉快地享受 `ESC` 键吧！

#### 文章到此结束

### 还不行？
若你遇到玄学问题，仍然概率性地失效。Hmmm，
请执行
```
xmodmap ~/.Xmodmap
```

若出现如下错误:
```
xmodmap:  $HOME/.Xmodmap:16:  bad keysym in remove modifier list
'Caps_Lock', no corresponding keycodes
xmodmap:  1 error encountered, aborting.
```
把
```
remove Lock = Caps_Lock
```
注释成

```
!remove Lock = Caps_Lock
```
再次

`xmodmap ~/.Xmodmap` 

## 参考
ArchLinuxWiki is the best!
