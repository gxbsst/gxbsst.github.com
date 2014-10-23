---
title: 如果使用ruby gem redis查看redis的keys
author: gxbsst
layout: post
permalink: /archives/553
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 270
views:
  - 104
categories:
  - Ruby/Ruby on Rails
---
<pre lang="ruby">irb(main):002:0> require 'rubygems'
=> true
irb(main):003:0> require 'redis'
=> true
irb(main):004:0> r = Redis.new
=> #&lt;Redis:0x8605b64 @sock=#&lt;TCPSocket:0x8605ab0>, @timeout=5, @port=6379, @db=0, @host="127.0.0.1">
irb(main):005:0> r.keys('*')

列出某个的key的值：

r.sort("Listen:1")



</pre>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [如果使用ruby gem redis查看redis的keys][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/553