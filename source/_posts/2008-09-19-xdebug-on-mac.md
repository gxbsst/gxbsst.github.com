---
title: Xdebug on Mac
author: gxbsst
layout: post
permalink: /archives/186
post_views_count:
  - 138
views:
  - 61
categories:
  - PHP
---
昨晚在自己mac装Xdebug，分享一下.

1. 原来我用pecl安装，但是不起作用，后面通<span style="font-family:STHeiti;">过编译安装</span>&#8230; 可以参考<span style="font-family:STHeiti;">这篇文章：</span> http://www.designified.com/blog/article/60/compiling-installing-xdebug-for-php-525-entropych-build-on-os-x-105?commented=0#txpCommentInputForm

* 注意你的php.ini里面的extension_dir,可以在phpinfo<span style="font-family:STHeiti;">查看，然后把</span>xdebug.so 复制到你<span style="font-family:STHeiti;">这个目录，我的目录是：</span> /usr/lib/php/extensions/  
* 在php.ini添加以下<span style="font-family:STHeiti;">语句，即载入模块</span>  
[xdebug]  
zend_extension=“/usr/lib/php/extensions/xdebug.so”

* 安装完<span style="font-family:STHeiti;">毕要重启服务器</span>: sudo apachectl restart

如果安装成功的<span style="font-family:STHeiti;">话，在</span>phpinfo<span style="font-family:STHeiti;">页面可以看到相关的信息</span>&#8230;.

<a href="http://www.weixuhong.com/content/uploads/2008/09/picture-1.png" onclick="window.open('http://www.weixuhong.com/content/uploads/2008/09/picture-1.png','popup','width=657,height=87,scrollbars=no,resizable=yes,toolbar=no,directories=no,location=no,menubar=no,status=yes,left=0,top=0');return false"><img src="http://www.weixuhong.com/content/uploads/2008/09/picture-1-tm.jpg" height="100" width="755" border="1" hspace="4" vspace="4" alt="Picture 1" title="Picture 1" /></a>

<a href="http://www.weixuhong.com/content/uploads/2008/09/picture-2.png" onclick="window.open('http://www.weixuhong.com/content/uploads/2008/09/picture-2.png','popup','width=859,height=513,scrollbars=no,resizable=yes,toolbar=no,directories=no,location=no,menubar=no,status=yes,left=0,top=0');return false"><img src="http://www.weixuhong.com/content/uploads/2008/09/picture-2-tm.jpg" height="100" width="167" border="1" hspace="4" vspace="4" alt="Picture 2" title="Picture 2" /></a>

2. 配置  
* 在php.ini添加以下

<pre lang="php">xdebug.default_enable = On
xdebug.show_exception_trace = On
xdebug.show_local_vars = 1
xdebug.max_nesting_level = 50
xdebug.var_display_max_depth = 6
xdebug.dump_once = On
xdebug.dump_globals = On
xdebug.dump_undefined = On
xdebug.dump.REQUEST = *
xdebug.dump.SERVER = REQUEST_METHOD,REQUEST_URI,HTTP_USER_AGENT

#跟踪自定<span style="font-family:STHeiti;">义</span>
xdebug.trace_format = 0
xdebug.auto_trace = On
xdebug.trace_output_dir = /tmp/traces
xdebug.trace_output_name = trace.%c.%p
xdebug.collect_params = 4
xdebug.collect_includes = On
xdebug.collect_return = On
xdebug.show_mem_delta = On
</pre>

<span style="font-family:STHeiti;">说明：</span>  
xdebug.dump\_once、xdebug.dump\_globals、xdebug.dump\_undefined 和 xdebug.dump\_SUPERGLOBAL <span style="font-family:STHeiti;">设置（其中</span> SUPERGLOBAL 可以是 COOKIE、FILES、GET、POST、REQUEST、SERVER 或 SESSION）用于控制哪些 PHP 超全局<span style="font-family:STHeiti;">变量将被包含在所有诊断结果中。</span>

　　将 xdebug.dump_globals <span style="font-family:STHeiti;">设为</span> On 以<span style="font-family:STHeiti;">转储名为</span> xdebug.dump_SUPERGLOBAL <span style="font-family:STHeiti;">设置中的超全局变量。例如，</span>xdebug.dump\_SERVER = REQUEST\_METHOD,REQUEST\_URI,HTTP\_USER_AGENT 将打印 PHP 超全局<span style="font-family:STHeiti;">变量</span> $\_SERVER['REQUEST\_METHOD']、$\_SERVER['REQUEST\_URI'] 和 $\_SERVER['HTTP\_USER_AGENT']。如果需要打印超全局<span style="font-family:STHeiti;">变量数组中的所有值，请使用星号</span> (\*)，例如 xdebug.dump_REQUEST=\*。如果<span style="font-family:STHeiti;">进一步将</span> xdebug.dump_undefined <span style="font-family:STHeiti;">设为</span> On 并且不<span style="font-family:STHeiti;">设定指定的超全局变量，则仍用值</span> undefined 打印<span style="font-family:STHeiti;">变量。</span>

　　即使捕捉到异常，代<span style="font-family:STHeiti;">码行</span> xdebug.show\_exception\_trace = On 仍将强制<span style="font-family:STHeiti;">执行异常跟踪。代码行</span> xdebug.show\_local\_vars = 1 将打印每个函数<span style="font-family:STHeiti;">调用的最外围中的所有局部变量，包括尚未初始化的变量。而</span> xdebug.var\_display\_max_depth = 6 表示<span style="font-family:STHeiti;">转储复杂变量的深度。</span>

<span style="font-family:STHeiti;">设定</span> xdebug.auto_trace = 1 将在<span style="font-family:STHeiti;">执行所有</span> PHP 脚本之前先<span style="font-family:STHeiti;">启用自动跟踪。另外，您可以通过代码设定</span> xdebug.auto\_trace = 0，并分别使用 xdebug\_start\_trace() 和 xdebug\_stop_trace() 函数<span style="font-family:STHeiti;">启用和禁用跟踪。但是，如果</span> xdebug.auto_trace <span style="font-family:STHeiti;">为</span> 1，<span style="font-family:STHeiti;">则可以在包括配置好的</span> auto\_prepend\_file 之前先<span style="font-family:STHeiti;">启动跟踪。</span>

<span style="font-family:STHeiti;">选项</span> xdebug.trace\_ouput\_dir 和 xdebug.trace\_output\_name 用于控制保存跟踪<span style="font-family:STHeiti;">输出的位置。在这里，所有文件都被保存到</span> /tmp/traces 中，并且每个跟踪文件都以 trace <span style="font-family:STHeiti;">为开头，后接</span> PHP 脚本的名称（%s）以及<span style="font-family:STHeiti;">进程</span> ID（%p）。所有 Xdebug 跟踪文件都以 .xt 后<span style="font-family:STHeiti;">缀结尾。</span>

　　默<span style="font-family:STHeiti;">认情况下，</span>Xdebug 将<span style="font-family:STHeiti;">显示时间、内存使用量、函数名和函数调用深度字段。如果将</span> xdebug.trace_format <span style="font-family:STHeiti;">设为</span> 0，<span style="font-family:STHeiti;">则输出将符合人类阅读习惯（将参数设为</span> 1 <span style="font-family:STHeiti;">则为机器可读格式）。此外，如果指定</span> xdebug.show\_mem\_delta = 1，<span style="font-family:STHeiti;">则可以查看内存使用量是在增加还是在减少，而如果指定</span> xdebug.collect_params = 4，<span style="font-family:STHeiti;">则可以查看传入参数的类型和值。要监视每个函数返回的值，请设定</span> xdebug.collect_return = 1。

3. 开始做个<span style="font-family:STHeiti;">测试</span>

<span style="font-family:STHeiti;">测试代码：</span>

<a href="http://www.weixuhong.com/content/uploads/2008/09/picture-4-1.png" onclick="window.open('http://www.weixuhong.com/content/uploads/2008/09/picture-4-1.png','popup','width=592,height=391,scrollbars=no,resizable=yes,toolbar=no,directories=no,location=no,menubar=no,status=yes,left=0,top=0');return false"><img src="http://www.weixuhong.com/content/uploads/2008/09/picture-4-1-tm.jpg" height="100" width="151" border="1" hspace="4" vspace="4" alt="Picture 4-1" /></a>

<span style="font-family:STHeiti;">结果：</span>

<a href="http://www.weixuhong.com/content/uploads/2008/09/picture-5.png" onclick="window.open('http://www.weixuhong.com/content/uploads/2008/09/picture-5.png','popup','width=1250,height=858,scrollbars=no,resizable=yes,toolbar=no,directories=no,location=no,menubar=no,status=yes,left=0,top=0');return false"><img src="http://www.weixuhong.com/content/uploads/2008/09/picture-5-tm.jpg" height="100" width="145" border="1" hspace="4" vspace="4" alt="Picture 5" /></a>

我<span style="font-family:STHeiti;">们可以看追踪文件：</span>/tmp/traces下的文件（可以看配置目<span style="font-family:STHeiti;">录</span>)  
用vim打开，但是有点不舒服，就是不是hightline的，但是你可以把xt.vim放到你.vim的配置文件下面，但是我的mac<span style="font-family:STHeiti;">还是不起作用，我需要在</span>vim 做set filetype=xt就可以了

<a href="http://www.weixuhong.com/content/uploads/2008/09/picture-7-1.png" onclick="window.open('http://www.weixuhong.com/content/uploads/2008/09/picture-7-1.png','popup','width=1280,height=800,scrollbars=no,resizable=yes,toolbar=no,directories=no,location=no,menubar=no,status=yes,left=0,top=0');return false"><img src="http://www.weixuhong.com/content/uploads/2008/09/picture-7-1-tm.jpg" height="100" width="160" border="1" hspace="4" vspace="4" alt="Picture 7-1" /></a>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Xdebug on Mac][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/186