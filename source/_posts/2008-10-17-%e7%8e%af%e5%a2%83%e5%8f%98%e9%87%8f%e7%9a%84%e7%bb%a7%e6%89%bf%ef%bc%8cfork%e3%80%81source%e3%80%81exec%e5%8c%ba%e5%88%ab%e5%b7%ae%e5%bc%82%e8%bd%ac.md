---
title: 环境变量的继承，fork、source、exec区别差异(转)
author: gxbsst
layout: post
permalink: /archives/210
post_views_count:
  - 136
views:
  - 52
categories:
  - Linux/Unix
  - 技术感想
---
* 这个对理解线程的环境相当有用，知道什么时候应该用fork，exec  
* 部分来自网上， 有部分是自己添加了注解&#8230;

<pre lang="lang">fork
   使用 fork 方式运行 script 时, 就是让 shell(parent process) 产生一个 child
   process 去执行该 script, 当 child process 结束后, 会返回 parent process,
   但 parent process 的环境是不会因 child process 的改变而改变的.

source
   使用 source 方式运行 script 时, 就是让 script 在当前 process 内执行, 而不
   是产生一个 child process 来执行. 由于所有执行结果均于当前 process 内完成,
   若 script 的环境有所改变, 当然也会改变当前 process 环境了.

exec
   使用 exec 方式运行script时, 它和 source 一样, 也是让 script 在当前process
   内执行, 但是 process 内的原代码剩下部分将被终止. 同样, process 内的环境随
   script 改变而改变.
</pre>

**结论：通常如果我们执行时，都是默认为fork的。大家可以通过pstree命令看看关于父子进程的关系。如上，如果想让父进程得到子进程的环境变量，就是source方式了。**

测试脚本练习：parent.sh

<pre lang="c">#!/bin/bash
A=B
echo “PID is parent.sh before child.sh :$$”
export A
echo “parent.sh: $A is $A => 这个来自父进程的变量, 而且是默认的...”
case $1 in
       fork)
               echo “using fork by default...1111111111”
               ./child.sh ;;
       source)
               echo “using source...”
               . ./child.sh ;;
       exec)
               echo “using exec...”
               exec ./child.sh ;;
esac
echo “PID is parent.sh after child.sh :$$”
echo “parent.sh: $A is $A 444444444 => 这个是来自父进程的变量...(如果用fork，这个应该是B,因为fork不影响父进程的环境...如果是source或者exec，这个应该是C,因为他们会影响到进程的环境....)”
</pre>

测试脚本练习：child.sh

<pre lang="c">#!/bin/bash
echo “PID for child.sh:$$”
echo “child.sh get $A=$A from parent.sh 22222222 => 这个是来自父进程的变量...”
A=C
export A
echo “child.sh: $A is $A 3333333 => 这个是来自子进程的变量....”
</pre>

执行结果

<pre lang="c">weston@life:/tmp$ ./parent.sh fork
PID is parent.sh before child.sh :5179
parent.sh: $A is B => 这个来自父进程的变量, 而且是默认的...
using fork by default...1111111111
PID for child.sh:5180
child.sh get $A=B from parent.sh 22222222 => 这个是来自父进程的变量...
child.sh: $A is C 3333333 => 这个是来自子进程的变量....
PID is parent.sh after child.sh :5179
parent.sh: $A is B 444444444 => 这个是来自父进程的变量...(如果用fork，这个应该是B,因为fork不影响父进程的环境...如果是source或者exec，这个应该是C,因为他们会影响到进程的环境....)
</pre>

<pre lang="c">PID is parent.sh before child.sh :5181
parent.sh: $A is B => 这个来自父进程的变量, 而且是默认的...
using source...
PID for child.sh:5181
child.sh get $A=B from parent.sh 22222222 => 这个是来自父进程的变量...
child.sh: $A is C 3333333 => 这个是来自子进程的变量....
PID is parent.sh after child.sh :5181
parent.sh: $A is C 444444444 => 这个是来自父进程的变量...(如果用fork，这个应该是B,因为fork不影响父进程的环境...如果是source或者exec，这个应该是C,因为他们会影响到进程的环境....)
</pre>

<pre lang="c">weston@life:/tmp$ ./parent.sh exec
PID is parent.sh before child.sh :5182
parent.sh: $A is B => 这个来自父进程的变量, 而且是默认的...
using exec...
PID for child.sh:5182
child.sh get $A=B from parent.sh 22222222 => 这个是来自父进程的变量...
child.sh: $A is C 3333333 => 这个是来自子进程的变量....
</pre>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [环境变量的继承，fork、source、exec区别差异(转)][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/210