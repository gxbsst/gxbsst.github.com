---
title: 在Dreamhost编译VIM
author: gxbsst
layout: post
permalink: /archives/221
post_views_count:
  - 107
views:
  - 54
categories:
  - Linux/Unix
---
1. 下载源文件（www.vim.org)  
2. 编译

<pre lang="c">#一定要指定  --prefix=/home/weston/user/local/ --enable-multibyte
# 一是要编译到目录（不然没有编译权限)，二是要支持fileencodings，不然你根本就不能输入中文
./configure --prefix=/home/weston/user/local/ --enable-multibyte
make 
make isntall
</pre>

3. 修改bin的地址

<pre lang="c">export EDITOR=“$HOME/user/local/bin/vim”
export VIMRUNTIME=“$HOME/share/vim”
</pre>

* 当然可以再配置你自己目录下的.vimrc

转载请注明：[韦旭红的点点滴滴][1] &raquo; [在Dreamhost编译VIM][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/221