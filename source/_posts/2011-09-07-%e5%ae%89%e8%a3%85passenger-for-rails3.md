---
title: 安装passenger for rails3
author: gxbsst
layout: post
permalink: /archives/557
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 245
views:
  - 102
categories:
  - Ruby/Ruby on Rails
---
<pre lang="c">gem install passenger

</pre>

<pre lang="c">yum install apr-devel
yum install apr-util-devel
yum install httpd-devel
</pre>

<pre lang="c">passenger-install-apache2-module
</pre>

复杂以下文件到httpd.conf

<pre lang="c">LoadModule passenger_module /usr/local/rvm/gems/ruby-1.9.2-p290-module/gems/passenger-3.0.9/ext/apache2/mod_passenger.so
   PassengerRoot /usr/local/rvm/gems/ruby-1.9.2-p290-module/gems/passenger-3.0.9
   PassengerRuby /usr/local/rvm/wrappers/ruby-1.9.2-p290-module/ruby
</pre>

<pre lang="c">#For PAIFAN 后台
&lt;VirtualHost *:80>
 ServerName padmin.qdigit.cn
 RailsEnv production
 #RailsEnv development 
 DocumentRoot /var/www/html/admin.insta/public
 ErrorLog /var/www/html/admin.insta/log/redmine.error.log
  &lt;Directory /var/www/html/admin.insta/public>
  AllowOverride all
  #Options -MultiViews           
  Options Indexes -MultiViews
 &lt;/Directory>
&lt;/VirtualHost>

</pre>

参考: http://www.modrails.com/install.html

转载请注明：[韦旭红的点点滴滴][1] &raquo; [安装passenger for rails3][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/557