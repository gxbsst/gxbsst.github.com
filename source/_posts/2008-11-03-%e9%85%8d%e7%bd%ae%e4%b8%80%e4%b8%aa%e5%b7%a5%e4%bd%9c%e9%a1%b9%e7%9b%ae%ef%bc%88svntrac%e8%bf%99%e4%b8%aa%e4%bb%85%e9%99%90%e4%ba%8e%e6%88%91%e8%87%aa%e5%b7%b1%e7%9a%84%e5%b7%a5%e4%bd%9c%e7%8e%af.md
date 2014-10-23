---
title: '配置一个工作项目（svn+trac)[这个仅限于我自己的工作环境)'
author: gxbsst
layout: post
permalink: /archives/213
post_views_count:
  - 119
views:
  - 32
categories:
  - 技术感想
---
建立svn版本

<pre lang="c">ssh baiselife
svnadmin create /home/weston/svn/colorunn.com
mkdir /home/weston/websites/colorunn.com/
svn import /home/weston/websites/colorunn.com/  file:///home/weston/svn/colorunn.com/project  --message=“Importing Project”
</pre>

#这个是在服务器上

<pre lang="c">svn co file:///home/weston/svn/colounn.com/project colorunn.com
</pre>

＃本机

<pre lang="c">svn co svn+ssh://baiselife/home/weston/svn/colorunn.com/project colorunn.com
</pre>

＃配置trac+svn

<pre lang="c">＃存放trac版本
trac-admin /home/weston/trac.weixuhong.com/colorunn.com initenv

# svn路径/home/weston/svn/colorunn.com

</pre>

<pre lang="c">cd ~/trac.weixuhong.com
cp linyufang.cgi colorunn.cgi
</pre>

#将linyufang.net替换成colorunn.com

<pre lang="c">vim colorunn.cgi 
</pre>

#修改默认utf8

<pre lang="c">vim colorunn.com/conf/trac.ini


将 default_charset = utf-8 
</pre>

访问 trac.weixuhogn.com

转载请注明：[韦旭红的点点滴滴][1] &raquo; [配置一个工作项目（svn+trac)[这个仅限于我自己的工作环境)][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/213