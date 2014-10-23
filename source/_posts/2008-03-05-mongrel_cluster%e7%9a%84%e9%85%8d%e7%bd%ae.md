---
title: 'mongrel_cluster的配置&#8230;'
author: gxbsst
layout: post
permalink: /archives/47
post_views_count:
  - 130
views:
  - 50
categories:
  - Ruby/Ruby on Rails
---
<div>
  在etc文件下建一个mongrel_cluster的文件夹，下面放一个配置文件：mongrel_cluster.yml<br />内容(不同的环境做不同的修改）：<br />&#8212;<br />cwd: /Users/weston/store<br />log_file: /Users/weston/store/log/mongrel.log<br />port: &#8220;8000&#8243;<br />environment: development<br />address: 127.0.0.1<br />pid_file: /Users/weston/store/tmp/pids/mongrel.pid<br />servers: 4</p> <p>
    2. 做个sym link 到Web程序，E.G： ln -s mongrel_cluster/mongrel_cluster.yml ~/store/config/mongrel_cluster.y<br />ml
  </p>
  
  <p>
    3. 启动mongrel_cluster
  </p>
  
  <p>
    sudo mongrel_cluster_stat
  </p>
  
  <p>
    (BTW,如果要知道Apache做前端代理：请看http://baiselife.com/bbs/thread-313-1-1.html 关于Apache的配置文件
  </p>
</div>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [mongrel_cluster的配置&#8230;][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/47