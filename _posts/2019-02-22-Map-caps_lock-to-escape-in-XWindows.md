---
layout:     post
title:      使用 xmodmap 交换 Esc 和 Caps Lock 按键
subtitle:   Map-caps_lock-to-escape-in-XWindows.md
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
### 折腾的环境和适用人群
环境是 ArchLinux 和 Xorg

以及 交换 Esc 和 Caps Lock 按键 对 vim user 来说十分重要

个人觉得 ohmyzsh+tmux+vim 及其各种插件效率非常高
[我的 dot 文件](https://github.com/junyixu/dotfiles)
### 方案 A
看系统按键映射可以输入：
Shell 代码

```
    xmodmap -pke
```

要交换 Esc 和 Caps Lock 按键，输入命令：```xmodmap -```，然后再输入：

Shell 代码

```
	clear Lock
    keysym Caps_Lock = Escape
    keysym Escape = Caps_Lock
    add Lock = Caps_Lock
```

第一行清除`CapsLock`的 Modifier 映射，第二行和第三行交换`Escape`和`Caps_Lock`的映射，最后一行加上对`CapsLock`的 Modifier 映射。

这样`Esc`就完成大写锁定的功能，而```CapsLock```则完成```Esc```的功能。但这种改变在电脑重启后失效了，为了让改变永久生效，将上述输入保存在文件```$HOME/.Xmodmap```下。
```
xmodmap ~/.Xmodmap
```


【注】 X 会在启动时按 /etc/X11/xinit/xinitrc 的要求去找 ~/.Xmodmap 这个文件
参考：[arch 关于 xmodmap 的 wiki](https://wiki.archlinux.org/index.php/Xmodmap)

以上就是我的方案 A：
在`~/.Xmodmap`写入

```
! 方案 A
clear Lock
keysym Caps_Lock = Escape
keysym Escape = Caps_Lock
add Lock = Caps_Lock
```
是的，方案 A 失败了……

我不明白失败的原因，现象是在我挂起或者休眠后在开启电脑时就会失效

然后，我尝试去`xmodmap ~/.Xmodmap`会报错：
第一个错误是

```
xmodmap:  /home/junyi/.Xmodmap:16:  bad keysym in remove modifier list
'Caps_Lock', no corresponding keycodes
xmodmap:  1 error encountered, aborting.
```
第二个错误说 Caps_Lock 与 Escape 找不到之类

### 方案 B
我在 [vim 论坛](http://vim.wikia.com/wiki/Map_caps_lock_to_escape_in_XWindows) 上找到了方案 B

```
! 方案 B
!remove Lock = Caps_Lock
!keysym Escape = Caps_Lock
!keysym Caps_Lock = Escape
!add Lock = Caps_Lock
```

挂起或休眠后还是失效，
`xmodmap ~/.Xmodmap` 后的报错也是一样的
可见`clear Lock`和`remove Lock = Caps_Lock`的效果是一样的

推测可能是 `Escape`和`Caps_Lock`交换时的问题
我决定使用`keycode`直接赋值

### 使用 keycode
通过
```
xmodmap -pke > ~/.Xmodmap
```
后直接把`9`和`66`互换，
`xmodmap ~/.Xmodmap` 后失败

现象是没有消除 `Lock` 键
按 `Caps_Lock` 后同时表现 `Escape`和“大小写锁定”的现象

### 方案 C
思索再三，最终方案是这样的
我删除了
`~/.Xmodmap`
```
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

挂起和休眠后还是会出现错误
这次表现为
键盘上的`Escape`和`Caps_Lock`同时表现`Escape`的效果
然后
`xmodmap ~/.Xmodmap`


这次只出现一条错误
即

```
xmodmap:  /home/junyi/.Xmodmap:16:  bad keysym in remove modifier list
'Caps_Lock', no corresponding keycodes
xmodmap:  1 error encountered, aborting.
```
我把
```
remove Lock = Caps_Lock
```
注释成

```
!remove Lock = Caps_Lock
```
再次

`xmodmap ~/.Xmodmap`
恢复正常

## 总结
```
! 方案 C
remove Lock = Caps_Lock
keycode  9 = Caps_Lock NoSymbol Caps_Lock
keycode  66 = Escape NoSymbol Escape
add Lock = Caps_Lock
```
是目前最好的方案了
休眠或挂起之后只需要把
```
remove Lock = Caps_Lock
```
注释后再
`xmodmap ~/.Xmodmap`
就可以了
