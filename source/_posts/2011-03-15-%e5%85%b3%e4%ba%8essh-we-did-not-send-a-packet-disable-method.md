---
title: 关于SSH we did not send a packet, disable method
author: gxbsst
layout: post
permalink: /archives/501
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 526
views:
  - 380
categories:
  - 技术感想
---
遇到这个问题一般是public key权限的问题， 一般修改服务器的.ssh 和 authorized_keys就可以解决问题了， 可以这样试一试:

chmod 700 .ssh  
chmod 700 .ssh/authorized_keys

也可以参考之前的文章:

http://weixuhong.com/技术感想/2008/04/26/ssh-不用密码/

转载请注明：[韦旭红的点点滴滴][1] &raquo; [关于SSH we did not send a packet, disable method][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/501