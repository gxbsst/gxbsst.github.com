---
title: Ruby long string block(ruby长字符串的处理)
author: gxbsst
layout: post
permalink: /archives/159
post_views_count:
  - 144
views:
  - 56
categories:
  - Ruby/Ruby on Rails
---
http://rubyluabridge.rubyforge.org/

*主要是为了使用long string，不用写些转义字符&#8230;

<pre lang="ruby">l.eval &lt;&lt;LUA_END
        n = 5                 -- see how Ruby long strings
        s = "hello"           -- make it easy to embed Lua code?
        a = { 1, 2, 3, 4 }
        h = { a='x', b='y', }
   LUA_END
   l.n       # => 5
   l.s       # => “hello”
   l.a       # => Lua::Table
   l.a[1]    # => 1
   l.h       # => Lua::Table
   l.h['a']  # => “x”
   l.h.a     # => “x”
</pre>

*当然这个LUA_END，主要是和下面的配对就行吧&#8230;.

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Ruby long string block(ruby长字符串的处理)][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/159