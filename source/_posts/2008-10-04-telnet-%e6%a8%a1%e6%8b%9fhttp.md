---
title: Telnet 模拟HTTP
author: gxbsst
layout: post
permalink: /archives/197
post_views_count:
  - 156
views:
  - 51
categories:
  - 技术感想
---
### 模拟GET方法

<pre lang="c">% telnet www.weixuhong.com 80
  Connected to www.wexiuhong.com.
  GET / HTTP/1.0                         [RETURN]
 Host linyufang.net
</pre>

### 模拟HEAD方法

<pre lang="c">% telnet www.weixuhong.com 80
  Connected to www.wexiuhong.com.
  HEAD / HTTP/1.0                         [RETURN]
</pre>

*记住要用大写  
*你可以模拟其他http方法，POST ， PUT， DELETE&#8230;.

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Telnet 模拟HTTP][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/197