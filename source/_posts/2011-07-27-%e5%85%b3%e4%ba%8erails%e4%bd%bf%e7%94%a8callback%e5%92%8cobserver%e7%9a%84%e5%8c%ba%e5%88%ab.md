---
title: 关于Rails使用Callback和Observer的区别
author: gxbsst
layout: post
permalink: /archives/547
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 276
views:
  - 136
categories:
  - Ruby/Ruby on Rails
---
可以参考：

http://stackoverflow.com/questions/1531514/observers-vs-callbacks

其中有一段是这样的：

<pre lang="ruby">class Model &lt; ActiveRecord::Base
  before_update :disallow_bob

  def disallow_bob
  return false if model.name == "bob"
  end
end

class ModelObserver &lt; ActiveRecord::Observer
  def before_update(model)
    return false if model.name == "mary"
  end
end

m = Model.create(:name => "whatever")

m.update_attributes(:name => "bob")
=> false -- name will still be "whatever" in database

m.update_attributes(:name => "mary")
=> true -- name will be "mary" in database
</pre>

Observers may only observe, they may not intervene.

转载请注明：[韦旭红的点点滴滴][1] &raquo; [关于Rails使用Callback和Observer的区别][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/547