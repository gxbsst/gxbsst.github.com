---
title: 'RuntimeError (!!! Missing the mysql2 gem. Add it to your Gemfile: gem &#8216;mysql2&#8242;):'
author: gxbsst
layout: post
permalink: /archives/533
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 186
views:
  - 89
categories:
  - Ruby/Ruby on Rails
---
在Rails3 出现这个错误，做以下工作:

1. 在Gemfile

<pre lang="ruby">gem 'mysql2', '~> 0.2.6'
</pre>

2.

<pre lang="ruby">bundle update
</pre>

3. 在datababse.yml

<pre lang="ruby">development:
  adapter: mysql2
  encoding: utf8
  database: devise
  # pool: 5
  username: root
  password:
  reconnect: true
  socket: /tmp/mysql.sock
  
</pre>

参考: http://stackoverflow.com/questions/4297253/install-mysql2-gem-on-snow-leopard-for-rails-3-with-rvm

转载请注明：[韦旭红的点点滴滴][1] &raquo; [RuntimeError (!!! Missing the mysql2 gem. Add it to your Gemfile: gem &#8216;mysql2&#8242;):][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/533