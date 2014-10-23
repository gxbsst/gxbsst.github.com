---
title: __call 通过一个类(Class)的实例（instance)调用另外一个class的实例的方法
author: gxbsst
layout: post
permalink: /2006/08/17/__call-%e9%80%9a%e8%bf%87%e4%b8%80%e4%b8%aa%e7%b1%bbclass%e7%9a%84%e5%ae%9e%e4%be%8b%ef%bc%88instance%e8%b0%83%e7%94%a8%e5%8f%a6%e5%a4%96%e4%b8%80%e4%b8%aaclass%e7%9a%84%e5%ae%9e%e4%be%8b%e7%9a%84/
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
 [2]: http://www.weixuhong.com/2006/08/17/__call-%e9%80%9a%e8%bf%87%e4%b8%80%e4%b8%aa%e7%b1%bbclass%e7%9a%84%e5%ae%9e%e4%be%8b%ef%bc%88instance%e8%b0%83%e7%94%a8%e5%8f%a6%e5%a4%96%e4%b8%80%e4%b8%aaclass%e7%9a%84%e5%ae%9e%e4%be%8b%e7%9a%84/