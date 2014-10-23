---
title: 在Dreamhost上使用svnmailer
author: gxbsst
layout: post
permalink: /archives/366
qzone:
  - 'true'
aktt_notify_twitter:
  - no
post_views_count:
  - 148
views:
  - 89
categories:
  - Linux/Unix
tags:
  - dreamhost
  - linux
  - svn
  - svnmailer
---
首先你要装好SVN,可以参考我以前的文章: <http://weixuhong.com/技术感想/2008/09/27/在dreamhost上配置trac-and-svn/>

svnmailer官方网站: <http://opensource.perlig.de>

<cite>svnmailer的作用就是当开发者，提交代码的时候，会给团队人员发送一份email，内容包括修改的文件及内容.</cite>



#### 1. 先下载一个svnmailer的版本

> <pre lang="c">wget http://storage.perlig.de/svnmailer/svnmailer-1.0.8.tar.gz
</pre>

#### 2. 安装svnmailer

> <pre lang="c">python setup.py install</pre>

#### 3. 生成svnmailer的配置文件

> 可在任何位置生成这个配置文件，这里我们在/home/weston/svn/svnmailer.conf,内容如下:  
> <cite></p> <pre lang="c">
[general]
smtp_host = localhost:25
config_charset = utf-8

[author table]
weston = youremail@gmail.com

[maps]
from_addr = [author table]
to_addr = [author table]

[defaults]
commit_subject_prefix = [svn] commit:
apply_charset_property = yes
show_applied_charset = yes
from_addr = %(author)s
to_addr   = weston
browser_base_url = Trac http://trac.weixuhong.com/red-cn.cgi/browser
mail_transfer_encoding = 8bit
</pre>
> 
> <p>
>   </cite>
> </p>
> 
> <p>
>   * 其中smtp_host = localhost:25是你发送email的smtp服务器<br /> * weston = youremail@gmail.com 是谁接收email
> </p></blockquote> 
> 
> <h4>
>   4. 配置项目，让svnmailer工作
> </h4>
> 
> <blockquote>
>   <p>
>     A. 首先到你的项目的hook文件夹下面，然后复制post-commit.tmpl 为post-commit，<br /><cite></p> <pre lang="c">cp post-commit.tmpl post-commit</pre>
>     
>     <p>
>       </cite>
>     </p></blockquote> 
>     
>     <blockquote>
>       <p>
>         B. 编辑post-commit文件,如下(具体可以看视频):<br /><cite></p> <pre lang="c">/home/weston/packages/bin/svn-mailer -c  -f /home/weston/svn/svnmailer.conf -e "UTF-8" -r "$2" -d "$1"</pre>
>         
>         <p>
>           </cite>
>         </p></blockquote> 
>         
>         <p>
>           转载请注明：<a href="http://www.weixuhong.com">韦旭红的点点滴滴</a> &raquo; <a href="http://www.weixuhong.com/archives/366">在Dreamhost上使用svnmailer</a>
>         </p>