---
layout:     post
title:      误删除 /boot 分区后修复 Arch Linux
subtitle:   after deleting boot by mistake
date:       2019-06-06
author:     Junix
header-img: img/post-bg-keybord.jpg
catalog: true
tags:
- Linux
- bootloader
- grub
- Windows10
---
# 修复引导
## 起因
我答应明天早晨分享我关于计算流体力学的拙见，已经在 onenote
上准备了相关资料，并准备用 surface 手写推导一些公式，我需要一个可以无线投屏的显
示屏(之前没买 Surface Mini DisplayPort).  
晚上去测试发现，学校的三星显示屏不支持无线投屏，为了信守诺言，我尝试把 surface
里的 windows10
无线投屏到我的笔记本电脑里的 windows10，再通过 HDMI 连接到三星显示屏。然而我的笔记本上的 windows10 是用超精简版的镜像装的，故要重装系统(反正里面也没啥东西)，然后手贱误操作把 arch 的 512M 的 `/boot/` 分区给删了。

## 慌张地去 archlinuxcn 群

立刻就有人回答，大家都很热心, 感动
![cuihao](/img/bootcuihao.png)

## 插上 archlinuxiso
开始敲命令：
```
# fdisk /dev/sda
```
发现原来的 /dev/sda1(boot分区) 没了，/dev/sda2(swap) 变成了 /dev/sda1，/dev/sda3(根分区) 变成了 /dev/sda2。

无奈：
```
# mkfs.vfat /dev/sda3
# mount /dev/sda2 /mnt
# mount /dev/sda2 /mnt/boot
# arch-chroot
```
## 重新装 /boot 下的包
![bootqu2](/img/bootqu2.png)  
 void001 老师这番操作太帅了！！！
 fc 老师提示在后面再加上 `pacman -S -`就可以了  
![pacman](/img/pacman.png)  
多亏了惠狐姐姐这一问，不然我还以为`-`是标准输出呢  
![awk1](/img/bootawk1.jpg)   
一切正常，我输入 y  
![awk2](/img/bootawk2.jpg)  
仙子问那个出错的文件是什么  
![awk3](/img/bootawk3.jpg)  
![awk4](/img/bootawk4.jpg)  
多谢仙子！

## 安装 grub 引导
群上的大神们用 systemd-boot, rEFInd 等等的各式 bootloader, 我是小白，笨拙地
``` 
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub
```
使用os-prober自动配置grub.cfg
```
# grub-mkconfig -o /boot/grub/grub.cfg
```
## 更改 fstab 里的 UUID
经过上述的操作后，重启，发现找不到盘了  
![fstab1](/img/bootfstab1.jpg)  
![fstab2](/img/bootfstab2.jpg)  
是 UUID 变了  
![UUID](/img/bootUUID.png)  
无奈，先修好再说：直接把 fstab 中的 boot分区的UUID 改成 /dev/sda3
## 显卡驱动
重启后屏幕颜色变了,额，重装显卡驱动(简单粗暴)
```
$ sudo pacman -S nvidia nvdia-utils
```
重启，熟悉的 arch，熟悉的 KDE

## 总结
1. 家中常备 archlinuxiso，arch 坏了可以修，win10 坏了可以重装
2. 没有 夏娜, 仙子，fc 等大神我是绝对不可能修好 /boot 分区的，以后还是多看 wiki，多读书，学习更多的知识是防震减灾的最好方式
3. 进行删分区等重要操作的时候一定要小心，“删”是一秒钟的事，“修”是一小时的事
