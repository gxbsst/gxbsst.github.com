---
title: Vim常用插件之vimpress
author: gxbsst
layout: post
permalink: /archives/250
post_views_count:
  - 117
views:
  - 45
categories:
  - Linux/Unix
tags:
  - VIM
---
今天介绍的一个插件是：vimpress， 这个是可以在vim下写blog的插件（限Wordpress)。  
参考: http://friggeri.net/blog/2007/07/13/vimpress

*安装这个插件，并且要运行正常，你的VIM得支持Phython，可以通过:python print &#8220;hello word&#8221;, 如果有输出，证明你的VIM是支持的，如果不支持，只能重新编译VIM了，如果在Mac下面，可以通过这样的命令重新安装VIM

<pre lang="bash">sudo port install vim +python
</pre>

下载vimpress

<pre lang="bash">cd ~/.vim
curl -O http://friggeri.net/download/vimpress.tar.gz
tar zxvf vimpress.tar.gz
</pre>

配置你的帐号

<pre lang="bash">vim ./plugin/blog.vim
*输入你正确的用户名和密码
</pre>

<pre lang="bash">Commands
":BlogList"
Lists all articles in the blog
":BlogNew"
Opens page to write new article
":BlogOpen id"
Opens the article for edition
":BlogSend"
Saves the article to the blog
Configuration
</pre>

通过以上命令，你就可以在vim写Blog了，很方便.

BTW, 还有一个插件好像叫BlogIt的，但是我测试，好像不支持中文，是在Title，经常出错，所以放弃，感觉vimpress比较好用:-)  
&#8211;EOF&#8211;

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Vim常用插件之vimpress][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/250