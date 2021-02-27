---
layout: post
title: 使用国内 vps 自建 Anki 同步服务
subtitle: Build-Anki-Sync-Server
date: 2021-02-19 21:14:11
author:     Junix
header-img: img/post-bg-miui6.jpg
catalog: true
tags:
- anki
- python
- android
---

## anki-sync-server

虽然 `poetry.lock`上写着`> = 3.8`，但是在 2021-02-19 只能用 python3.8, python3.9会[报错](https://github.com/ankicommunity/anki-sync-server/issues/73) (具体原因我没深入调查)。

2021-02-19 用 docker 安装也无法成功。

### 安装

先克隆下来
```
$ cd ~
$ git clone https://github.com/ankicommunity/anki-sync-server.git
```
原先的仓库被移动的理由参见这条 [issue](https://https://github.com/tsudoko/anki-sync-server/issues/70)

### 我用 pyenv 管理 python 版本

我的 vps 是 archlinux, 用 pacman 安装 pyenv 和其插件：
```
# pacman -S pyenv-virtualenv
```

安装 python3.8
```
$ pyenv install 3.8.7
```
然后
```sh
$ cd anki-sync-server
$ pyenv local 3.8.7
$ pyenv virtualenv anki-server
$ pyenv activate anki-server 
```

再按照它的 [README](https://https://github.com/ankicommunity/anki-sync-server) 装依赖和启动模块

### 用 systemd 开机启动

```
$ cd ~/.config/systemd/user
$ vi anki_sync_server.service
```

写入
```
[Unit]
Description=anki_sync_server Service
After=network.target

[Service]
ExecStart=/bin/sh -c 'eval "$(pyenv init -)" && cd ~/anki-sync-server/src && pyenv activate anki-server && python -m ankisyncd'        

[Install]
WantedBy=default.target
```
```
systemctl --user enable --now anki_sync_server.service
```

## 按照 README 配置 anki 客户端

### 解决 ankidroid 报错的问题
```
java.net.UnknownServiceException: CLEARTEXT communication to *** not permitted by network security policy
```

网上搜了搜，原因如下

Google:
> 为保证用户数据和设备的安全，Google针对下一代 Android 系统(Android P) 的应用程序，将要求默认使用加密连接，这意味着 Android P 将禁止 App 使用所有未加密的连接，因此运行 Android P 系统的安卓设备无论是接收或者发送流量，未来都不能明码传输。

针对这个问题，有以下三种解决方法：
1. APP 改用 https 请求
2. `targetSdkVersion` 降到27以下
3. 更改网络安全配置

前面两个方法容易理解和实现，具体说说第三种方法，更改网络安全配置

先从 github 下载最新版 ankidroid
```
$ wget -c https://github.com/ankidroid/Anki-Android/releases/download/v2.14.3/AnkiDroid-2.14.3-arm64-v8a.apk
```
下载 android-apktool 解包
```
# pacman -S android-apktool
$ apktool -d AnkiDroid-2.14.3-arm64-v8a.apk
```
会得到一个 `AnkiDroid-2.14.3-arm64-v8a` 目录
```
$ vim AnkiDroid-2.14.3-arm64-v8a/res/xml/network_security_config.xml
```
删除原有内容并写入：
```
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true" />
</network-security-config>
```
构建 apk
```
$ apktool -b AnkiDroid-2.14.3-arm64-v8a
```
生成签名(随便输入点什么):
```
$ keytool -genkey -alias demo.keystore -keyalg RSA -validity 40000 -keystore demo.keystore
```
签名 apk：
```
$ jarsigner -verbose -keystore demo.keystore AnkiDroid-2.14.3-arm64-v8a/dist/AnkiDroid-2.14.3-arm64-v8a.apk demo.keystore
```
也可以不签名，使用 xposed 的`核心破解`模块
