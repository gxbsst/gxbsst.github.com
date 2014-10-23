---
title: 在firebug显示mysql query
author: gxbsst
layout: post
permalink: /archives/400
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 129
views:
  - 58
categories:
  - PHP
---
用下面debug\_mysql\_query这个函数代替mysql_query

<pre lang="php">if (!function_exists('debug_mysql_query')) {
 
    function debug_mysql_query($query)
    {
        $js_query = str_replace(array('\', "'"), array("\\", "\'"), $query);
        $js_query = preg_replace('#([x00-x1F])#e', '"x" . sprintf("%02x", ord("1"))', $js_query);
        echo ''."n";
        return mysql_query($query);
    }
}
</pre>

<img src="http://www.weixuhong.com/content/uploads/2010/01/螢幕快照-2010-01-07-3.30.54-PM.png" alt="螢幕快照 2010-01-07 3.30.54 PM.png" border="0" width="1016" height="77" />

转载请注明：[韦旭红的点点滴滴][1] &raquo; [在firebug显示mysql query][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/400