---
layout: post
title:  我的 KDE 及其全家桶的配置
subtitle: My KDE Config
date: 2021-02-28 21:43:33
author:     Junix
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
- KDE
---
以下个人配置，具有强烈的个人偏见，如果有哪些地方你认为不妥，欢迎评论。

## 全局 meta
设置 `->` 窗口管理 `->`窗口行为 `->` 窗口操作 把 `alt` 改为 `meta`，很多程序如 inkscape, blender, `alt` 是有其他作用的。

注意：如果你使用 tiled menu `alt+右键` 调整窗口大小变为 `meta+右键` 调整窗口大小。

## konsole

我的很多应用，如 konsole 已经配置好了，不需要使用菜单，日常将菜单收起来，免得占地方。
如果用亮色微风，而 konsole 用暗色主题的话，标题栏白色很刺眼，使用`alt+F3`选择更多动作，为 konsole 设置特殊程序规则可以使标题栏变成黑色。

若想要设置 vim 和 konsole 一样的配色，可以用 KDE 自带的取色器 KColorChooser 取相同背景色，调节 konsole 为半透明，就可以让 konsole 和 vim 一起变成半透明。

## dolphin

### 远程传输
直接在地址栏输入 `fish://user@domain/folder` 和dolphin自带的分屏一起使用，就可以远程传输文件。

### 单击选中
系统设置 `->` 工作区行为 `->` 常规行为 `->` 点击文件夹或文件时选中他们

### 预览
```
# pacman -S kdegraphics-thumbnailers
```
为 pdf 等文件开启预览视图。

## 窗口管理
我在不同的虚拟桌面，完成不同的任务。

### 在相同的虚拟桌面切换窗口
`Alt + ~` 切换相同程序的窗口 `Alt + Tab` 切换不同程序的窗口，并且长按 `Alt + Tab` 不动，可以用鼠标在左侧点击以选中窗口，这和 windows 的行为类似。然而，有的时候，当前虚拟桌面窗口数量多，我又不想使用鼠标，这时，我使用 meta + O 快捷键(在系统设置`->`快捷键里面), 然后敲程序的字母，过滤窗口，Enter 选中窗口。


## 在不同的虚拟桌面切换窗口

用鼠标移动到屏幕左上角的触发角(四个角都可以配置功能)平铺所有虚拟桌面的所有窗口，敲字母以程序名称进行选择。而我的 linux 几乎一个月才关机一次(得益于游戏本可扩展内存，而且现在内存白菜价)，我嫌平铺的窗口太多，所以把左上角的触发角设置为平铺当前虚拟桌面的功能，而用 krunner 通过敲程序名在不同的虚拟桌面过滤窗口。

## 触摸板
我对触摸板不是很感冒，更爱使用快捷键。

Linux 对触摸板的支持比起 Mac OS 差远了，但是使用
`pacman -S libinput-gestures`
基本可以达到 windows 10 触摸板的体验。

由于儿时长期用 windows 打游戏，我始终相信鼠标是十分符合人体工学的东西，该用就用。

## 用 latte dock 作为底栏
长按 meta(win键) 显示数字和其他快捷键，比如我使用 `meta(win) + m` 唤出 mathematica，使用 `meta + 8` 唤出终端，左手大拇指向里按，右手中指直接伸直按8，相当快，平时 konsole 不关闭，用的时候直接唤起。

* Global: 应用的选择用底栏实现；
* Local: 程序内部的菜单在上部，而部分程序不需要菜单，可以平时把菜单收起来
* 而 blender, inkscape, photoshop 这类程序需要侧栏的按钮，不宜和 Global 混淆
这种方式比较符合我的直觉。

## 某个窗口程序卡住怎么办
如 plasmashell 卡死，可以用
```sh
$ kquitapp5 plasmashell
$ kstart5 plasmashell
```
命令来重启。

## F11
有些程序自带 `F11` 表示全屏，如 chromium，可以把 KDE 默认设置全屏快捷键改成 `Alt+F11`

## OCR
系统设置`->` 自定义快捷键，使用 `Meta+r`(Recognition) 使用自己糊的[OCR](https://github.com/junyixu/baidu_ocr)。

## KDE 主题

我非常喜欢亮色微风的古朴风，突出了内容；`canta-kde` 的背景颜色太白太过刺眼，反客为主，干扰视线。

我日常使用暗色微风，其和 windows 10 的让人瞎眼暗色主题形成了鲜明的对比。但是仍有很少量的程序对暗色微风支持得不好，如 anki, wps，我们可以

先调好白色主题，然后

```sh
$ cp ~/.config ~/whiteconfig
```

再变为暗色主题，
最后修改其 desktop 文件，如 wps 表格

```sh
$ cp /usr/share/applications/wps-office-et.desktop ~/.local/share/applications/wps-office-et.desktop
```
把
```
[Desktop Entry]
Comment=Use WPS Spreadsheets to analyze manage data.
Comment[zh_CN]=使用WPS表格分析、管理数据
Exec=/usr/bin/et %F
GenericName=WPS Spreadsheets
GenericName[zh_CN]=WPS 表格
MimeType=application/wps-office.et;application/wps-office.ett;application/wps-office.ets;application/wps-office.eto;application/wps-office.xls;application/wps-office.xlt;application/vnd.ms-excel;application/msexcel;application/x-msexcel;application/wps-office.xlsx;application/wps-office.xltx;application/vnd.openxmlformats-officedocument.spreadsheetml.sheet;application/wps-office.uos;
Name=WPS Spreadsheets
Name[zh_CN]=WPS 表格
StartupNotify=false
Terminal=false
Type=Application
Categories=Office;Spreadsheet;Qt;
X-DBUS-ServiceName=
X-DBUS-StartupType=
X-KDE-SubstituteUID=false
X-KDE-Username=
Icon=wps-office2019-etmain
InitialPreference=3
StartupWMClass=et
```

修改成

```
[Desktop Entry]
Comment=Use WPS Spreadsheets to analyze manage data.
Comment[zh_CN]=使用WPS表格分析、管理数据
Exec=XDG_CONFIG_HOME=/home/USERNAME/whiteconfig /usr/bin/et %F
GenericName=WPS Spreadsheets
GenericName[zh_CN]=WPS 表格
MimeType=application/wps-office.et;application/wps-office.ett;application/wps-office.ets;application/wps-office.eto;application/wps-office.xls;application/wps-office.xlt;application/vnd.ms-excel;application/msexcel;application/x-msexcel;application/wps-office.xlsx;application/wps-office.xltx;application/vnd.openxmlformats-officedocument.spreadsheetml.sheet;application/wps-office.uos;
Name=WPS Spreadsheets
Name[zh_CN]=WPS 表格
StartupNotify=false
Terminal=false
Type=Application
Categories=Office;Spreadsheet;Qt;
X-DBUS-ServiceName=
X-DBUS-StartupType=
X-KDE-SubstituteUID=false
X-KDE-Username=
Icon=wps-office2019-etmain
InitialPreference=3
StartupWMClass=et
```
即在`Exec=`前面加上环境变量来在整体暗色主题的情况下让个别程序使用亮色主题。

你可以用二分法在`~/whiteconfig`里面找到那个主题有关的文件，把里面有和主题无关的文件删了(找到后可以告诉我)。由于我的硬盘足够大，就没有去找了。
