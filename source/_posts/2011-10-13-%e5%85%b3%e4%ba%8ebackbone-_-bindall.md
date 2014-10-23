---
title: 关于backbone _.bindAll
author: gxbsst
layout: post
permalink: /archives/563
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 295
views:
  - 141
categories:
  - Javascript
  - 技术感想
tags:
  - Javascript
---
<pre lang="javasript">_.bindAll(this, 'render');
			this.model.bind('change', this.render);

</pre>

以上这两行代码主要为了当model改变时， view执行render， 那_.bindAll有什么用呢？

看这里：http://stackoverflow.com/questions/6079055/why-do-bindall-in-backbone-js-views

其中有一段是这样的：

<pre>Without _.bindAll( this, 'render' ) when model changes this in render will be pointing to the model, not to the view, so we won't have neither this.el nor this.$ or any other view's properties available.
</pre>

当model被change时， this指向model, 但是我们要执行render, 那么就需要_.bindAll(this, &#8216;render&#8217;)， 使model也有这个render的方法？

请达人解答?

*  
新版本这样就可以

this.model.bind(&#8216;change&#8217;, this.render, this);

<img style="display:block; margin-left:auto; margin-right:auto;" src="http://www.weixuhong.com/content/uploads/2011/10/Screen-Shot-2011-10-14-at-1.55.50-PM.png" alt="Screen Shot 2011-10-14 at 1.55.50 PM.png" border="0" width="406" height="567" />



<img style="display:block; margin-left:auto; margin-right:auto;" src="http://www.weixuhong.com/content/uploads/2011/10/Screen-Shot-2011-10-14-at-2.06.54-PM.png" alt="Screen Shot 2011-10-14 at 2.06.54 PM.png" border="0" width="600" height="352" />



<img style="display:block; margin-left:auto; margin-right:auto;" src="http://www.weixuhong.com/content/uploads/2011/10/Screen-Shot-2011-10-14-at-2.18.03-PM.png" alt="Screen Shot 2011-10-14 at 2.18.03 PM.png" border="0" width="417" height="590" />



<img style="display:block; margin-left:auto; margin-right:auto;" src="http://www.weixuhong.com/content/uploads/2011/10/Screen-Shot-2011-10-14-at-3.31.51-PM.png" alt="Screen Shot 2011-10-14 at 3.31.51 PM.png" border="0" width="600" height="432" />



<img style="display:block; margin-left:auto; margin-right:auto;" src="http://www.weixuhong.com/content/uploads/2011/10/Screen-Shot-2011-10-14-at-3.33.11-PM.png" alt="Screen Shot 2011-10-14 at 3.33.11 PM.png" border="0" width="600" height="380" />



<img style="display:block; margin-left:auto; margin-right:auto;" src="http://www.weixuhong.com/content/uploads/2011/10/Screen-Shot-2011-10-17-at-5.20.27-PM.png" alt="Screen Shot 2011-10-17 at 5.20.27 PM.png" border="0" width="600" height="332" />



<img style="display:block; margin-left:auto; margin-right:auto;" src="http://www.weixuhong.com/content/uploads/2011/10/Screen-Shot-2011-10-18-at-3.37.23-PM.png" alt="Screen Shot 2011-10-18 at 3.37.23 PM.png" border="0" width="600" height="378" />

转载请注明：[韦旭红的点点滴滴][1] &raquo; [关于backbone _.bindAll][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/563