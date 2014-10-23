---
title: 在 Ubuntu 中启用 Mod_rewrite 模块
author: gxbsst
layout: post
permalink: /archives/71
post_views_count:
  - 96
views:
  - 25
categories:
  - 技术感想
---
需要用到 Apache 的 Mod_rewrite 模块。在 Ubuntu 中可以使用下面的方法来开启它。

启用 Mod_rewrite 模块

在终端中执行 sudo a2enmod rewrite 指令后，即启用了 Mod_rewrite 模块。

另外，也可以通过将 /etc/apache2/mods-available/rewrite.load 连接到 /etc/apache2/mods-enabled/rewrite.load 来打开 Mod_rewrite 模块。用指令操作就是：  
sudo ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load

一点小提示

事实上，当我在 Ubuntu 中采用上述做法并重启了 Apache 服务后，仍然无法正常 rewrite 网址。这里，还有一点需要注意的地方：  
sudo vim /etc/apache2/sites-enabled/000-default

将其中的：  
AllowOverride None

修改为：  
AllowOverride All

上面的 /etc/apache2/sites-enabled/000-default 实则为 /etc/apache2/sites-available/default 的连接。而 AllowwOverride None 则会完全忽略 .htaccess 文件，自然其中所定义的 rewrite 规则也就不能生效了。

最后，别忘了使用下列指令来重启 Apache:  
sudo /etc/init.d/apache2 restart

转载请注明：[韦旭红的点点滴滴][1] &raquo; [在 Ubuntu 中启用 Mod_rewrite 模块][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/71