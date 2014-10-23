---
title: Yii不同Model使用不同的数据库(Multiple Database)
author: gxbsst
layout: post
permalink: /archives/256
post_views_count:
  - 133
views:
  - 67
categories:
  - PHP
---
在Yii如果其中有一个Model需要链接到不同的数据库，我可以重写getDbConnection这个方法：  
比如我在Product这个model里面这样设置:

<pre lang="php">public function getDbConnection()
  {
    $db = new CDbConnection('mysql:host=localhost;dbname=store', 'root', '');
    $db->active = true;
    return $db;
  }
</pre>

但是如果要在behavior里面实现呢？那我们可以试一试!  
经过在Behavior添加，没有发现成功，是不是有其他的方法呢？期待&#8230;

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Yii不同Model使用不同的数据库(Multiple Database)][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/256