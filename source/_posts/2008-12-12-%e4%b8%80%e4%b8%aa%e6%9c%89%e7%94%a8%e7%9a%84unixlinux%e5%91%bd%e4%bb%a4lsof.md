---
title: 一个有用的Unix/Linux命令(lsof)
author: gxbsst
layout: post
permalink: /archives/224
post_views_count:
  - 113
views:
  - 59
categories:
  - Linux/Unix
---
lsof（list open files）是一个列出当前系统打开文件的工具。在linux环境下，任何事物都以文件的形式存在，通过文件不仅仅可以访问常规数据，还可以访问网络连接和硬件。所以如传输控制协议 (TCP) 和用户数据报协议 (UDP) 套接字等，系统在后台都为该应用程序分配了一个文件描述符，无论这个文件的本质如何，该文件描述符为应用程序与基础操作系统之间的交互提供了通用接口。因为应用程序打开文件的描述符列表提供了大量关于这个应用程序本身的信息，因此通过lsof工具能够查看这个列表对系统监测以及排错将是很有帮助的。

lsof使用实例

恢复删除的文件

当Linux计算机受到入侵时，常见的情况是日志文件被删除，以掩盖攻击者  
的踪迹。管理错误也可能导致意外删除重要的文件，比如在清理旧日志时，  
意外地删除了数据库的活动事务日志。有时可以通过lsof来恢复这些文件。

当进程打开了某个文件时，只要该进程保持打开该文件，即使将其删除，  
它依然存在于磁盘中。这意味着，进程并不知道文件已经被删除，它仍然  
可以向打开该文件时提供给它的文件描述符进行读取和写入。除了该进程  
之外，这个文件是不可见的，因为已经删除了其相应的目录索引节点。  
在/proc 目录下，其中包含了反映内核和进程树的各种文件。/proc目录挂  
载的是在内存中所映射的一块区域，所以这些文件和目录并不存在于磁盘  
中，因此当我们对这些文件进行读取和写入时，实际上是在从内存中获取  
相关信息。大多数与 lsof 相关的信息都存储于以进程的 PID 命名的目录中  
，即 /proc/1234 中包含的是 PID 为 1234 的进程的信息。每个进程目录中  
存在着各种文件，它们可以使得应用程序简单地了解进程的内存空间、文  
件描述符列表、指向磁盘上的文件的符号链接和其他系统信息。lsof 程序  
使用该信息和其他关于内核内部状态的信息来产生其输出。所以lsof 可以  
显示进程的文件描述符和相关的文件名等信息。也就是我们通过访问进程  
的文件描述符可以找到该文件的相关信息。 

当系统中的某个文件被意外地删除了，只要这个时候系统中还有进程正在  
访问该文件，那么我们就可以通过lsof从/proc目录下恢复该文件的内容。 假如由于误操作将/var/log/messages文件删除掉了，那么这时要将/var/log/messages文件恢复的方法如下：  
首先使用lsof来查看当前是否有进程打开/var/logmessages文件，如下：  
\# lsof |grep /var/log/messages  
syslogd 1283 root 2w REG 3,3 5381017 1773647 /var/log/messages (deleted)  
从上面的信息可以看到 PID 1283（syslogd）打开文件的文件描述符为 2。  
同时还可以看到/var/log/messages已经标记被删除了。因此我们可以在  
/proc/1283/fd/2 （fd下的每个以数字命名的文件表示进程对应的文件描  
述符）中查看相应的信息，如下：  
\# head -n 10 /proc/1283/fd/2  
Aug 4 13:50:15 holmes86 syslogd 1.4.1: restart.  
Aug 4 13:50:15 holmes86 kernel: klogd 1.4.1, log source = /proc/kmsg started.  
Aug 4 13:50:15 holmes86 kernel: Linux version 2.6.22.1-8 (root@everestbuilder.linux-ren.org) (gcc version 4.2.0) #1 SMP Wed Jul 18 11:18:32 EDT 2007  
Aug 4 13:50:15 holmes86 kernel: BIOS-provided physical RAM map:  
Aug 4 13:50:15 holmes86 kernel: BIOS-e820: 0000000000000000 &#8211; 000000000009f000 (usable)  
Aug 4 13:50:15 holmes86 kernel: BIOS-e820: 000000000009f000 &#8211; 00000000000a0000 (reserved)  
Aug 4 13:50:15 holmes86 kernel: BIOS-e820: 0000000000100000 &#8211; 000000001f7d3800 (usable)  
Aug 4 13:50:15 holmes86 kernel: BIOS-e820: 000000001f7d3800 &#8211; 0000000020000000 (reserved)  
Aug 4 13:50:15 holmes86 kernel: BIOS-e820: 00000000e0000000 &#8211; 00000000f0007000 (reserved)  
Aug 4 13:50:15 holmes86 kernel: BIOS-e820: 00000000f0008000 &#8211; 00000000f000c000 (reserved)  
从上面的信息可以看出，查看 /proc/8663/fd/15 就可以得到所要恢复的数  
据。如果可以通过文件描述符查看相应的数据，那么就可以使用 I/O 重定  
向将其复制到文件中，如:  
cat /proc/1283/fd/2 > /var/log/messages  
对于许多应用程序，尤其是日志文件和数据库，这种恢复删除文件的方法  
非常有用。 

更多细节请看: http://blog.csdn.net/guoguo1980/archive/2008/04/24/2324454.aspx

转载请注明：[韦旭红的点点滴滴][1] &raquo; [一个有用的Unix/Linux命令(lsof)][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/224