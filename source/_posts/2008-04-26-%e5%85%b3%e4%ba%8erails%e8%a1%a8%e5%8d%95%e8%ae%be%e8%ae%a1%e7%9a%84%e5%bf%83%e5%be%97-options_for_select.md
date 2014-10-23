---
title: 关于rails表单设计的心得——options_for_select
author: gxbsst
layout: post
permalink: /archives/57
post_views_count:
  - 104
views:
  - 42
categories:
  - Ruby/Ruby on Rails
---
<span style="font-family:STHeiti;">这段时间做了公司的</span>cms,需要用到很多的表<span style="font-family:STHeiti;">单，其中需要用到</span>options\_for\_select，但是上网<span style="font-family:STHeiti;">查了很多资料，给我提供的</span>example都不能解决我的<span style="font-family:STHeiti;">问题，一下是我常用的</span>options\_for\_select的例子，希望<span style="font-family:STHeiti;">对朋友有帮助：</span>

注意下面的@news.headline\_position.to\_s，<span style="font-family:STHeiti;">这是要显示</span>options的selected.

<%= select\_tag &#8216;news[headline\_position]&#8216;, options\_for\_select(%w{1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 },@news.headline\_position.to\_s) % >

<%= select\_tag &#8216;news[beta\_visible]&#8216;, options\_for\_select({ &#8216;hiden&#8217; => &#8217;1&#8242;,&#8217;display&#8217; =>&#8217;0&#8242; },@news.beta_visible) %>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [关于rails表单设计的心得——options\_for\_select][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/57