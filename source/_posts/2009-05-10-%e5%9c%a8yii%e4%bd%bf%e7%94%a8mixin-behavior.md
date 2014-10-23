---
title: '在Yii使用Mixin &#8211; Behavior'
author: gxbsst
layout: post
permalink: /archives/257
post_views_count:
  - 201
views:
  - 69
categories:
  - Javascript
  - Linux/Unix
  - PHP
  - Regular Expressions
  - Ruby/Ruby on Rails
  - Xhtml/css
  - 工作计划
  - 心情随写
  - 技术感想
---
我们知道Ruby有Mixin的功能，可以扩展类的实例方法或者类方法，只需要include就可以做这样的事情，但是PHP好像没有这样好用的方法？但是在Yii有这样的方法，怎么实现呢？

下面有一个例子:

<pre lang="php">Yii::app()->fileCache->attachBehavior('EFileCacheBehavior', array('class'=>'EFileCacheBehavior'));

</pre>

如果要在App启动的时候就能永这个EFileCacheBehavior,可以在Main.php配置这个文件&#8230;

<pre lang="php">'fileCache'=>array(
            'class'=>'application.extensions.filecache.EFileCache',
            'autoCleanExpiredCache'=>false,
            'behaviors'=>array(
                'EFileCacheBehavior'=>array(
                    'class'=>'EFileCacheBehavior',
                ),
            ),
        ), 
</pre>

这样就可以扩展的方法了。  
就是说如果EFileCacheBehavior有一个方法叫test();  
那么你就可以通过：  
Yii::app()->fileCache->test()调用。

转载请注明：[韦旭红的点点滴滴][1] &raquo; [在Yii使用Mixin &#8211; Behavior][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/257