---
title: objective-c enum 与 typedef
author: gxbsst
layout: post
permalink: /archives/529
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 129
views:
  - 45
categories:
  - IOS
---
今天看到enum 和 typedef， 在两个小节中书中分别出现了2个例子，如下  
enum direction {north, south, east, west};  
typedef enum {north, south, east, west} direction;  
不禁产生疑问，这两个有什么区别，仔细对照了一下，发现是这样的：  
大同小异，  
同： 都是申明了一个枚举类型。  
异：在使用该枚举类型定义变量的时候，语法不一样，举例如下： 

<pre lang="c">1  enum direction {north, south, east, west};    
3  enum direction facing = north;  
4 
5  typedef enum {north, south, east, west} direction;     
7  direction facing = north; 
</pre>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [objective-c enum 与 typedef][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/529