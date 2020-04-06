---
layout: post
title: 自动唤起挂起状态的 Linux
subtitle: automatically wake linux system from sleep
date: 2020-04-06 12:13:39
author:   junyi
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
- linux
---

博客长草了，来水一篇。

## 目标

我想要在早上六点用 `you-get` 下载 b 站视频。

## 方法

学校 23 点熄灯，我的笔记本撑死 3 小时续航。笔记本的 bios 是阉割版的，没有电源管理，不能实现定时开机。

笔记本挂起，一晚上大概只需要用 20% 的电。
用 rtcwake 从挂起状态自动开机无疑是个好选择。

## 写脚本

```
# vim /usr/local/bin/wake.sh
```
```
#! /bin/bash
rtcwake -m mem -l -t $(date +%s -d 'tomorrow 06:30')
```
```
# vim /etc/systemd/system/wake.service
```
```
[Unit]
Description=wake Service

[Service]
ExecStart=/usr/local/bin/wake.sh

[Install]
WantedBy=default.target
```
```
[Unit]
Description=Run wake at 23.58 daily

[Timer]
OnCalendar=23:58

[Install]
WantedBy=timers.target
```

## 遇到的问题
由于用了 vdpau，我的
`~/.local/share/sddm/xorg-session.log` 长到了 32 G，
`df -h` 后我的 `/` 还剩 900 M，为了保持 arch 的 uptime，lsof 后把用这个文件的进程都 kill 了

没找到解决办法，暂时把这个文件链接到 `/dev/null`。
