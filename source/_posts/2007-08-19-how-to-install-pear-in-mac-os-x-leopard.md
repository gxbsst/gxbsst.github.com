---
title: How To Install PEAR in Mac OS X Leopard
author: gxbsst
layout: post
permalink: /archives/167
post_views_count:
  - 183
views:
  - 74
categories:
  - PHP
---
Unlike previous version of OS X, Leopard doesn&#8217;t come with PHP&#8217;s PEAR repository installed by default. Luckily, installing is quick and painless. From a command line:

view plaincopy to clipboardprint?  
*curl http://pear.php.net/go-pear > go-pear.php  
sudo php -q go-pear.php *  
(Just press enter to select all the default choices.)

Next we need to modify our php.ini file to include the new PEAR files:

view plaincopy to clipboardprint?  
*sudo cp /etc/php.ini.default /etc/php.ini  
Edit /etc/php.ini and change*

view plaincopy to clipboardprint?  
*;include_path = “.:/php/includes” *  
to read

view plaincopy to clipboardprint?  
*include_path = “.:/usr/share/pear” *  
Restart Apache and you&#8217;re done!

* 更新

1. 在console显示pecl, pear命令

在 .bash_profile 添加  
PATH=“$PATH:/usr/share/pear/bin”

这样你就可以用pear, pecl安装包了

e.g. sudo pecl install pecl_http

转载请注明：[韦旭红的点点滴滴][1] &raquo; [How To Install PEAR in Mac OS X Leopard][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/167