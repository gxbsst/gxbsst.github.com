---
title: 配置RT的rt-mailgate在Postfix , Extmail
author: gxbsst
layout: post
permalink: /archives/487
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 291
views:
  - 105
categories:
  - 心情随写
---
请参考这个地方配置：

http://www.ptitov.net/2008/07/request-tracker-installation-o.html

但是在Rt-mailgate这个地方遇到了问题， 主要是alias的问题， 只要需要在email服务器设置别名就可以了  
如：

<div style="text-align:center;">
  <img src="http://www.weixuhong.com/content/uploads/2010/10/概述_.jpg" alt="概述_.jpg" border="0" width="772" height="111" />
</div>

然后配置： /etc/postfix/aliases

添加如下行：

rt: &#8220;|/opt/rt3/bin/rt-mailgate &#8211;queue General &#8211;action correspond &#8211;url http://rt.icooking.me&#8221;

就可以了。

记得执行: newaliases

参考：

http://wiki.bestpractical.com/view/PostFixSQLAliasProblem

转载请注明：[韦旭红的点点滴滴][1] &raquo; [配置RT的rt-mailgate在Postfix , Extmail][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/487