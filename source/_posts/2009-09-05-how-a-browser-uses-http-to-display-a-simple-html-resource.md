---
title: how a browser uses HTTP to display a simple HTML resource
author: gxbsst
layout: post
permalink: /archives/272
post_views_count:
  - 121
views:
  - 62
categories:
  - Xhtml/css
---
* <span style="font-family:STHeiti;">这</span>个是来自《<span style="font-family:serif;">HTTP The Definitive Guide</span>》的解<span style="font-family:STHeiti;">释</span>，当然<span style="font-family:STHeiti;">这</span>个只是<span style="font-family:STHeiti;">层</span>面上的解<span style="font-family:STHeiti;">释</span>，如果要理解底<span style="font-family:STHeiti;">层</span>的<span style="font-family:STHeiti;">知识，应该看《unix网络编程><br /> </span>  
(a)  
The browser extracts the server&#8217;s hostname from the URL.

(b)  
The browser converts the server&#8217;s hostname into the server&#8217;s IP address.

(c)  
The browser extracts the port number (if any) from the URL.

(d)  
The browser establishes a TCP connection with the web server.

(e)  
The browser sends an HTTP request message to the server.

(f)  
The server sends an HTTP response back to the browser.

(g)  
The connection is closed, and the browser displays the document.

<img src="http://www.weixuhong.com/content/uploads/2009/09/Picture-2-1.png" height="484" width="606" border="1" hspace="4" vspace="4" alt="Picture 2-1" />

转载请注明：[韦旭红的点点滴滴][1] &raquo; [how a browser uses HTTP to display a simple HTML resource][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/272