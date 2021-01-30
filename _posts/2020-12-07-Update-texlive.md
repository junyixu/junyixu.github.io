---
layout:     post
title:      升级 texlive
subtitle:   Update texlive
date:       2020-12-07
author:     Junix
header-img: img/post-bg-keybord.jpg
tags:
- latex
---

## 覆盖文件

`cd` 到你装 texlive 的位置
```
$ cd /usr/local/texlive/
```
由于我的文件系统是 btrfs, 直接
```
# mv 2019 2020
```
下载 sh 文件(若网慢请用国内镜像)：
```
# wget http://mirror.ctan.org/systems/texlive/tlnet/update-tlmgr-latest.sh
```

执行以下命令

请去公园跑圈步，回来后它也就跑完了
```
# sh update-tlmgr-latest.sh -- --upgrade
# tlmgr update --self --all
```
更新 lua 字体数据库
```
# luaotfload-tool -fu
```

## 更改环境变量
### 更改家里的环境变量
只需要把第一行 2019
```
export TEXLIVE=/usr/local/texlive/2019
export PATH=$TEXLIVE/bin/x86_64-linux:$PATH
export MANPATH=$TEXLIVE/texmf-dist/doc/man:$MANPATH
export INFOPATH=$TEXLIVE/texmf-dist/doc/info:$INFOPATH
```
改为 2020 即可
```
export TEXLIVE=/usr/local/texlive/2020
export PATH=$TEXLIVE/bin/x86_64-linux:$PATH
export MANPATH=$TEXLIVE/texmf-dist/doc/man:$MANPATH
export INFOPATH=$TEXLIVE/texmf-dist/doc/info:$INFOPATH
```

### 更改 root 的环境变量
```
$ sudo -E EDITOR=vim visudo
```
把 secure_path 的 2019 改为 2020
