---
title: Configuration of DRBD on CentOS5.2 with XEN
author: gxbsst
layout: post
permalink: /archives/151
post_views_count:
  - 146
views:
  - 83
categories:
  - 技术感想
---
以下文章是我的同事Flanker(flankeroot@gmail.com)先生在深夜<span style="font-family:STHeiti;">实现的，其中他翻阅了很多</span>manual，都不能<span style="font-family:STHeiti;">实现，以下是他试验的过程</span>.  
*如果有任何疑<span style="font-family:STHeiti;">问</span>可以<span style="font-family:STHeiti;">发</span>Email<span style="font-family:STHeiti;">给</span>他，或者在本网站留言&#8230;.

1. 好<span style="font-family:STHeiti;">处</span>  
不用RAID1就可以<span style="font-family:STHeiti;">实现</span>RAID的功能，可以<span style="font-family:STHeiti;">节约很多钱呢</span>&#8230;

2. 配置<span style="font-family:STHeiti;">过程</span>

<pre lang="c">Hostname: Server
IPAddress: 10.0.0.60

# fdisk -l
/dev/sda1               1          37      297171   83  Linux
/dev/sda2              38         391     2843505   83  Linux
# wget ftp://zid-luxinst.uibk.ac.at/pub/dist/centos/5/extras/x86_64/RPMS/kmod-drbd-xen-8.0.12-1.2.6.18_92.1.6.el5.x86_64.rpm
# wget ftp://zid-luxinst.uibk.ac.at/pub/dist/centos/5/extras/x86_64/RPMS/drbd-8.0.12-1.el5.centos.x86_64.rpm
# rpm -i drbd-8.0.12-1.el5.centos.x86_64.rpm
# rpm -i kmod-drbd-xen-8.0.12-1.2.6.18_92.1.6.el5.x86_64.rpm
# insmod /lib/modules/2.6.18-92.1.6.el5xen/extra/drbd/drbd.ko
# vi /etc/drbd.conf
===================
resource r0 {
protocol C;
startup {
}
disk {
on-io-error   detach;
}
net {
cram-hmac-alg sha1;
shared-secret “FooFunFactory”;
allow-two-primaries;
}
syncer {
rate 10M;
}
on server {
device     /dev/drbd0;
disk       /dev/sda2;
address    10.0.0.60:7788;
meta-disk  internal;
#    meta-disk  /dev/sda1[0];
}
on server1 {
device     /dev/drbd0;
disk       /dev/sda2;
address    10.0.0.61:7788;
meta-disk  internal;
#    meta-disk  /dev/sda1[0];
}
}

===============================
# modprobe drbd
# drbdadm create-md r0
# drbdadm adjust r0
# cat /proc/drbd
# /etc/init.d/drbd start



Hostname: Server1
IPAddress: 10.0.0.61
# fdisk -l
/dev/sda1               1          37      297171   83  Linux
/dev/sda2              38         391     2843505   83  Linux
# vi /etc/drbd.conf
===================
resource r0 {
protocol C;
startup {
}
disk {
on-io-error   detach;
}
net {
cram-hmac-alg sha1;
shared-secret “FooFunFactory”;
allow-two-primaries;
}
syncer {
rate 10M;
}
on server {
device     /dev/drbd0;
disk       /dev/sda2;
address    10.0.0.60:7788;
meta-disk  internal;
#    meta-disk  /dev/sda1[0];
}
on server1 {
device     /dev/drbd0;
disk       /dev/sda2;
address    10.0.0.61:7788;
meta-disk  internal;
#    meta-disk  /dev/sda1[0];
}
}
===============================
# modprobe drbd
# drbdadm create-md r0
# drbdadm adjust r0
# /etc/init.d/drbd start
# cat /proc/drbd

Change to Server
# /etc/init.d/ddrbdsetup /dev/drbd0 primary -o
# cat /proc/drbd
----------------
version: 8.0.12 (api:86/proto:86)
GIT-hash: 5c9f89594553e32adb87d9638dce591782f947e3 build by buildsvn@c5-x8664-build, 2008-06-26 19:32:09
0: cs:SyncSource st:Primary/Secondary ds:UpToDate/Inconsistent C r---
ns:28488 nr:0 dw:0 dr:28880 al:0 bm:1 lo:82 pe:233 ua:180 ap:0
[&gt;....................] sync'ed:  1.2% (2815820/2843380)K
finish: 0:15:18 speed: 3,060 (3,060) K/sec
resync: used:1/61 hits:14190 misses:2 starving:0 dirty:0 changed:2
act_log: used:0/127 hits:0 misses:0 starving:0 dirty:0 changed:0
rbd start
----------------
* At the same time
[root@server1 ~]# cat /proc/drbd
version: 8.0.12 (api:86/proto:86)
GIT-hash: 5c9f89594553e32adb87d9638dce591782f947e3 build by buildsvn@c5-x8664-build, 2008-06-26 19:32:09
0: cs:SyncTarget st:Secondary/Primary ds:Inconsistent/UpToDate C r---
ns:0 nr:300964 dw:300324 dr:0 al:0 bm:18 lo:160 pe:224 ua:160 ap:0
[=&gt;..................] sync'ed: 10.8% (2543056/2843380)K
finish: 0:12:42 speed: 3,212 (3,228) K/sec
resync: used:1/61 hits:150527 misses:19 starving:0 dirty:0 changed:19
act_log: used:0/127 hits:0 misses:0 starving:0 dirty:0 changed:0
* Here wait a few mins
[root@server ~]# cat /proc/drbd
-------------------------------
version: 8.0.12 (api:86/proto:86)
GIT-hash: 5c9f89594553e32adb87d9638dce591782f947e3 build by buildsvn@c5-x8664-build, 2008-06-26 19:32:09
0: cs:Connected st:Primary/Secondary ds:UpToDate/UpToDate C r---
ns:2843380 nr:0 dw:0 dr:2843380 al:0 bm:174 lo:0 pe:0 ua:0 ap:0
resync: used:0/61 hits:1421516 misses:174 starving:0 dirty:0 changed:174
act_log: used:0/127 hits:0 misses:0 starving:0 dirty:0 changed:0
-------------------------------


Change to Server1
[root@server1 ~]# cat /proc/drbd
---------------------------------
version: 8.0.12 (api:86/proto:86)
GIT-hash: 5c9f89594553e32adb87d9638dce591782f947e3 build by buildsvn@c5-x8664-build, 2008-06-26 19:32:09
0: cs:Connected st:Secondary/Primary ds:UpToDate/UpToDate C r---
ns:0 nr:2843380 dw:2843380 dr:0 al:0 bm:174 lo:0 pe:0 ua:0 ap:0
	resync: used:0/61 hits:1421516 misses:174 starving:0 dirty:0 changed:174
	act_log: used:0/127 hits:0 misses:0 starving:0 dirty:0 changed:0
---------------------------------
# drbdsetup /dev/drbd0 primary
# cat /proc/drbd
----------------
version: 8.0.12 (api:86/proto:86)
GIT-hash: 5c9f89594553e32adb87d9638dce591782f947e3 build by buildsvn@c5-x8664-build, 2008-06-26 19:32:09
0: cs:Connected st:Primary/Primary ds:UpToDate/UpToDate C r---
ns:0 nr:2843380 dw:2843380 dr:0 al:0 bm:174 lo:0 pe:0 ua:0 ap:0
	resync: used:0/61 hits:1421516 misses:174 starving:0 dirty:0 changed:174
	act_log: used:0/127 hits:0 misses:0 starving:0 dirty:0 changed:0
-----------------
* Now at the same time
[root@server ~]# cat /proc/drbd
version: 8.0.12 (api:86/proto:86)
GIT-hash: 5c9f89594553e32adb87d9638dce591782f947e3 build by buildsvn@c5-x8664-build, 2008-06-26 19:32:09
0: cs:Connected st:Primary/Primary ds:UpToDate/UpToDate C r---
ns:2843380 nr:0 dw:0 dr:2843380 al:0 bm:174 lo:0 pe:0 ua:0 ap:0
resync: used:0/61 hits:1421516 misses:174 starving:0 dirty:0 changed:174
	act_log: used:0/127 hits:0 misses:0 starving:0 dirty:0 changed:0
--------------------------------

Testing
[root@server ~]# /etc/init.d/drbd restart &#38;&#38; [root@server1 ~]# /etc/init.d/drbd restart
[root@server ~]# drbdsetup /dev/drbd0 primary -o
[root@server1 ~]# drbdsetup /dev/drbd0 primary
[root@server ~]# mkfs.ext3 /dev/drbd0
[root@server ~]# mount /dev/drbd0 /mnt
[root@server ~]# date &gt; /mnt/server
[root@server ~]# umount /mnt
[root@server1 ~]# mount /dev/drbd0 /mnt &#38;&#38; ls /mnt
lost+found  server
[root@server1 mnt]# date &gt; server1
[root@server1 ~]# umount /mnt
[root@server ~]# mount /dev/drbd0 /mnt &#38;&#38; ls /mnt
lost+found  server  server1

Notes: It shouldn't mount the drbd0 at the same time on both nodes

</pre>

3. 以下是<span style="font-family:STHeiti;">配置文件</span>

<pre lang="c">resource r0 {
protocol C;
startup {
}
disk {
on-io-error   detach;
}
net {
cram-hmac-alg sha1;
shared-secret “FooFunFactory”;
allow-two-primaries;
}
syncer {
rate 10M;
}
on server {
device     /dev/drbd0;
disk       /dev/sda2;
address    10.0.0.60:7788;
meta-disk  internal;
#    meta-disk  /dev/sda1[0];
}
/etc/drbd.conf
</pre>

<a href="http://www.weixuhong.com/content/uploads/2008/07/drbd.txt" onclick="window.open('http://www.weixuhong.com/content/uploads/2008/07/drbd.txt','popup','width=160,height=112,scrollbars=no,resizable=yes,toolbar=no,directories=no,location=no,menubar=no,status=yes,left=0,top=0');return false"><img src="http://www.weixuhong.com/content/uploads/2008/07/drbd-tm.jpg" height="100" width="142" border="1" hspace="4" vspace="4" alt="Drbd" /></a>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Configuration of DRBD on CentOS5.2 with XEN][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/151