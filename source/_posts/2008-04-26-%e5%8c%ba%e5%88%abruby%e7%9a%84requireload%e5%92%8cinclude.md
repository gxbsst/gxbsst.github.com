---
title: 区别Ruby的require,load,和include
author: gxbsst
layout: post
permalink: /archives/121
post_views_count:
  - 128
views:
  - 46
categories:
  - Ruby/Ruby on Rails
---
相同之处：三者均在kernel中定义的，均含有包含进某物之意。

不同之处：

1、requre,load用于文件，如.rb等等结尾的文件。

2、include则用于包含一个文件(.rb等结尾的文件)中的模块。

3、requre一般情况下用于加载库文件，而load则用于加载配置文件。

4、requre加载一次，load可加载多次。

怎么样，简单吧！再看个例子。

如果说abc.rb中包含一个模块Ma，和几个类Ca,Cb等等。那么你若想在ef.rb文件中使用abc.rb中的资源，你得这样:

require &#8216;abc.rb&#8217;

若还想在ef.rb的某个类中使用abc.rb中的模块，则应在这个类中加入

include Ma

如果你只想在ef.rb文件的某个类中使用abc.rb的模块，你得这样：

require &#8216;abc.rb&#8217;

include Ma

这两句就告诉了你它们区别。

下面部分摘自于：http://anw.stikipad.com/ocean/show/require+load+and+include  
Ruby 中 “require”, “load” 和 “include” 有甚麼不同呢? “require” 和 “load” 用途是一致的, 用來載入新的程式庫, “include” 是用來 mix-in 模組.

“require” 可載入某個 a.rb 檔案, 且可以省略 ”.rb”. 而且它只會在第一次的時候載入, 若再次 “require” 時就會忽略

require &#8216;a&#8217;

a = A.new

“load” 和 “require” 一樣但要用 a.rb 全名, 且每次一定會重新載入

load &#8216;a.rb&#8217;

a = A.new

載入程式庫的順序呢(類似 java class path)? Ruby 把這個資訊存在 ”$:” 系統全域變數上, 你可以藉著 RUBYLIB 或 ruby -I 來加入新的載入目錄.

puts $:

“include” 用來 mix-in 某個模組, 可以減少書寫的長度

require &#8216;webrick&#8217;  
include WEBrick

//可以不用 server = WEBrick::HTTPServer.new(&#8230;)  
server = HTTPServer.new(&#8230;)

转载请注明：[韦旭红的点点滴滴][1] &raquo; [区别Ruby的require,load,和include][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/121