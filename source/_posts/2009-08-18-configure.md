---
title: configure
author: gxbsst
layout: post
permalink: /archives/260
post_views_count:
  - 114
views:
  - 47
categories:
  - Linux/Unix
  - PHP
---
在RedHat AS4 安装http://blog.s135.com/nginx\_php\_v5/遇到的一个libpng的问题

下载了其中的rpm，安装但是编译php的时候老是遇到configure: error: png.h not found.的问题

我到/usr/src/redhat/SOURCES/找到  
libpng-1.2.7.tar.bz2

1. tar jxvf libpng-1.2.7.tar.bz2 

2. cp scripts/makefile.std makefile

3. make

4. make install

这个问题才解决

不知道rpm安装为什么不成功&#8230;

转载请注明：[韦旭红的点点滴滴][1] &raquo; [configure][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/260