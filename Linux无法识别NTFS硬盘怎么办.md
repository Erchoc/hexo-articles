---
title: Linux无法识别NTFS硬盘怎么办
date: 2016-12-15 00:36:42
tags: linux
---

> 在桌面版的CentOS使用过程中发现系统无法识别我NTFS格式的移动硬盘，一番搜索后才发现这是因为windows系统常用的硬盘格式是NTFS，和linux下使用的ext系列格式是完全不兼容的。需要挂载到指定目录才能正常访问这个移动硬盘。

> 开源世界的力量强大，直接造就了ntfs-3g这个软件包。我们安装后即可打开NTFS硬盘并读写其中的数据,但是默认的yum源没有ntfs-3g包,并且该软件包依赖于fuse库.这样的话我们还是来编译安装ntfs-3g这个软件吧。

<!-- more -->

```
yum search fuse

yum install fuse -y

wget http://tuxera.com/opensource/ntfs-3g_ntfsprogs-2016.2.22.tgz

tar -zxvf tar ntfs-3g_ntfsprogs-2016.2.22.tgz

cd ntfs-3g_ntfsprogs-2016.2.26

./configure

make

make install
```
