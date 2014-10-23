---
title: pc与mac的共享上网路线图（双网卡）
author: gxbsst
layout: post
permalink: /archives/111
post_views_count:
  - 142
views:
  - 55
categories:
  - 技术感想
---
http://www.macx.cn/A/A.asp?B=89&ID=84157

1.注意:一定要<span style="font-family:STHeiti;">设</span>XP的IP地址<span style="font-family:STHeiti;">为</span>192.168.0.1;2.苹果的无<span style="font-family:STHeiti;">线网设为自动获取</span>IP,3.<span style="font-family:STHeiti;">应该是</span>mac<span style="font-family:STHeiti;">创建网络</span>,然后PC<span style="font-family:STHeiti;">连接到</span>MAC,

大家好！  
我<span style="font-family:STHeiti;">终于把家里的</span>pc与小白一起共享上网了。我截了<span style="font-family:STHeiti;">图划个路线，希望给还在苦苦找方法互联</span>pc与mac的fans有些帮助。<span style="font-family:STHeiti;">废话不说了－－－－－》</span>go！  
我家的条件：  
<span style="font-family:STHeiti;">软件</span>: sygate office networks4.851  
mac: 10.4.2系<span style="font-family:STHeiti;">统</span>  
pc: xp sp2；双网卡，其中一个是无<span style="font-family:STHeiti;">线网卡，另一个网卡连接</span>lan，上网要虚<span style="font-family:STHeiti;">拟拨号，如图</span>  
<span style="font-family:STHeiti;">图片</span>193720.jpg

<span style="font-family:STHeiti;">宽带连接就是连网线的网卡；</span>  
<span style="font-family:STHeiti;">长城宽带是用来虚拟拨号的。</span>

开始<span style="font-family:STHeiti;">设置：</span>  
1、<span style="font-family:STHeiti;">连互联网的宽带连接网卡设置：</span>

<span style="font-family:STHeiti;">图片</span>194155.jpg

并且在高<span style="font-family:STHeiti;">级里设置：</span>

<span style="font-family:STHeiti;">图片</span>194240.jpg

2、无<span style="font-family:STHeiti;">线网卡用来和小白组局域网，设置如下：</span>  
网卡要开<span style="font-family:STHeiti;">启</span>ad-hoc功能  
<span style="font-family:STHeiti;">设置</span>ssid名称（密<span style="font-family:STHeiti;">码随便），便于小白开</span>airport<span style="font-family:STHeiti;">查找，以及</span>

<span style="font-family:STHeiti;">图片</span>194357.jpg

高<span style="font-family:STHeiti;">级里面就不要设置共享了</span>

3、虚<span style="font-family:STHeiti;">拟拨号的</span>“<span style="font-family:STHeiti;">长城宽带</span>”就不要<span style="font-family:STHeiti;">设置了，自动获取</span>ip好了，高<span style="font-family:STHeiti;">级里面也不要设置共享</span>  
<span style="font-family:STHeiti;">设置的话可能要把前面</span>1、2步<span style="font-family:STHeiti;">骤的设置改掉了</span>

4、<span style="font-family:STHeiti;">设置小白，新小白的</span>airport派用<span style="font-family:STHeiti;">场了，很简单：</span>

<span style="font-family:STHeiti;">这个自动吧</span>  
<span style="font-family:STHeiti;">图片</span>  
195525.jpg  
<span style="font-family:STHeiti;">这个也是自动吧</span>

<span style="font-family:STHeiti;">图片</span>  
195627.jpg

5、好了，小白搜索到了pc了吧？  
<span style="font-family:STHeiti;">这里，</span>pc可<span style="font-family:STHeiti;">设置共享的盘、文件夹等等，小白这样就可以找到，如下</span>  
(sorry，机器出状况了，finder不响<span style="font-family:STHeiti;">应了，重启再来）</span>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [pc与mac的共享上网路线图（双网卡）][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/111