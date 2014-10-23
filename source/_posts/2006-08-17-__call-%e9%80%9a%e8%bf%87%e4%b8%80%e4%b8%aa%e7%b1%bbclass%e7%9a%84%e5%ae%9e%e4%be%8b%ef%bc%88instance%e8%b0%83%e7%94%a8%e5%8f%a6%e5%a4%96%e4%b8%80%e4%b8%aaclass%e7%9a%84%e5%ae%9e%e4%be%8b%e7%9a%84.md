---
title: __call 通过一个类(Class)的实例（instance)调用另外一个class的实例的方法
author: gxbsst
layout: post
permalink: /archives/166
post_views_count:
  - 113
views:
  - 54
categories:
  - PHP
---
<img src="http://www.weixuhong.com/content/uploads/2008/08/picture-7.png" height="678" width="533" border="1" align="left" hspace="4" vspace="4" alt="Picture 7" />

<div style="clear:both;">
</div>

通过一下几行代码，类HelloWorldDelegator就可以调用HelloWorld的所有实例方法  
function __construct()  
{  
20 $this->obj = new HelloWorld();  
21 }  
22  
23 function __call($method, $args)  
24 {  
25 return call\_user\_func_array(array($this->obj, $method), $args);  
26 }  
27  
28 private $obj;  
}

转载请注明：[韦旭红的点点滴滴][1] &raquo; [__call 通过一个类(Class)的实例（instance)调用另外一个class的实例的方法][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/166