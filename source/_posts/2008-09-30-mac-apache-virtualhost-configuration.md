---
title: 'Mac Apache VirtualHost Configuration&#8230;.'
author: gxbsst
layout: post
permalink: /archives/191
post_views_count:
  - 130
views:
  - 59
categories:
  - 技术感想
---
比如要添加1个local域名：  
linyufang.local

1. 首先要编辑/etc/hosts文件

<pre lang="c">sudo vim /etc/hosts

</pre>

添加这个一行

<pre lang="c">127.0.0.1 linyufang.local
</pre>

2. 配置httpd.conf

<pre lang="c">sudo vim /etc/apache2/httpd.conf
</pre>

输入以下内容

<pre lang="c">NameVirtualHost *:80
&lt;VirtualHost *:80>
  #ServerAdmin dns@red.com
  ServerName linyufang.local
  DocumentRoot /Users/weston/projects/beautyonly.net
  Options +Indexes
  ErrorLog /tmp/error.log
  CustomLog /tmp/access.log combined
  &lt;Directory /Users/weston/projects/linyufang.net>
    Options Indexes FollowSymLinks MultiViews Includes
    AllowOverride All
    Order allow,deny
    allow from all
  &lt;/Directory>
&lt;/VirtualHost>
</pre>

3. 重启apache  
sudo apachectl restart

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Mac Apache VirtualHost Configuration&#8230;.][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/191