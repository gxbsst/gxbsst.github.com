---
title: rails 3.1 Mountable Engines 使用方法
author: gxbsst
layout: post
permalink: /archives/551
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 270
views:
  - 149
categories:
  - Ruby/Ruby on Rails
---
在了解 Moutable之前， 先看这个视频：

http://railscasts.com/episodes/277-mountable-engines

了解Mountable Engines与Full Engines的区别， 看这篇文章:

http://stackoverflow.com/questions/6118905/rails-3-1-engine-vs-mountable-app

当我们使用：

<pre lang="ruby">rails plugin new uhoh --mountable
</pre>

我们可以把这个创建好的plugin变成一个gem来使用。

比如我们可以先创建一个rails app

<pre lang="ruby">rails new with_engine -T -O -J
</pre>

编辑Gemfile, 添加以下一行:

<pre lang="ruby">gem 'uhoh', :path => '/Users/weston/Downloads/277-mountable-engines/uhoh-after/' #刚才创建的mountable 路径

</pre>

执行

<pre lang="ruby">bundle install 

vim config/routs.rb
</pre>

添加以下一行:

<pre lang="ruby">mount Uhoh::Engine => "/uhoh", :as => "uhoh_engine"
</pre>

这样我们就可以使用这个engines了&#8230;

转载请注明：[韦旭红的点点滴滴][1] &raquo; [rails 3.1 Mountable Engines 使用方法][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/551