---
title: Ruby on Rails项目文件目录结构和环境设置
author: gxbsst
layout: post
permalink: /archives/107
post_views_count:
  - 129
views:
  - 49
categories:
  - Ruby/Ruby on Rails
---
Ruby on Rails<span style="font-family:STHeiti;">项目文件目录结构</span>  
README <span style="font-family:STHeiti;">说明文档</span>  
Rakefile 生成脚本  
app/ 存放<span style="font-family:STHeiti;">项目的</span>Model, View和Controller等文件  
components/ 存放可重复使用的<span style="font-family:STHeiti;">组件</span>, <span style="font-family:STHeiti;">现在已经不大使用</span>  
config/ 配置文档及数据<span style="font-family:STHeiti;">库连接配置文档</span>  
db/ 存放数据<span style="font-family:STHeiti;">库</span>schema和migration信息  
doc/ 存放自<span style="font-family:STHeiti;">动生成的文档</span>  
lib/ 存放在Model, View和Controller<span style="font-family:STHeiti;">间共享的代码</span>  
<span style="font-family:STHeiti;">为方便整理</span>,不同功能的代<span style="font-family:STHeiti;">码可放到其不同的子目录下</span>.

<span style="font-family:STHeiti;">调用</span>sub\_dir下的my\_lib_code.rb代<span style="font-family:STHeiti;">码的方法为</span>: require &#8220;sub\_dir/my\_lib_code&#8221;  
log/ 存放程序生成的日志文件  
里面有三个最主要的log<span style="font-family:STHeiti;">为</span>:development.log, test.log和production.log,分别<span style="font-family:STHeiti;">对应不同的运行环境</span>.  
public/ 存放<span style="font-family:STHeiti;">对网络公开的文件</span>  
script/ 存放脚本工具  
不<span style="font-family:STHeiti;">带参数直接运行大多数的脚本工具可以显示出相应的使用帮助信息</span>.  
常<span style="font-family:STHeiti;">见的</span>script:  
about  
breakpointer  
destroy<=>generate  
server  
script/performance/benchmarker  
test/ <span style="font-family:STHeiti;">测试工具</span>  
tmp/ 存放<span style="font-family:STHeiti;">临时文件</span>, 如<span style="font-family:STHeiti;">缓存</span>, session, socket&#8230;  
vendor/ 存放外来代<span style="font-family:STHeiti;">码</span>, 如外来插件, 也可用来放rails<span style="font-family:STHeiti;">构架本身</span>, 以使rails兼容不同版本需求的程序.

<span style="font-family:STHeiti;">运行环境</span>  
使用-e XXXX切<span style="font-family:STHeiti;">换运行环境</span>:  
ruby script/server -e production #默<span style="font-family:STHeiti;">认为</span>development

配置数据<span style="font-family:STHeiti;">库参数</span>  
修改config/database.yml文件

配置<span style="font-family:STHeiti;">环境</span>  
修改config/environment.rb文件.

命名<span style="font-family:STHeiti;">规范</span>  
所有<span style="font-family:STHeiti;">变量以小写字母单词命名</span>,<span style="font-family:STHeiti;">单词间用下划线</span>&#8220;\_&#8221;分隔. 如order\_status  
所有class和module以大写开<span style="font-family:STHeiti;">头的单词命名</span>,<span style="font-family:STHeiti;">单词间直接连接</span>,如: LineItem

数据<span style="font-family:STHeiti;">库中所有表格命名形式同变量名</span>,且全<span style="font-family:STHeiti;">为复数形式</span>,如:orders  
所有文件名命名形式也同<span style="font-family:STHeiti;">变量名</span>

Rails可推<span style="font-family:STHeiti;">论相关文件名</span>, 所以在框架内可以<span style="font-family:STHeiti;">节省很多</span>require &#8220;xxx&#8221;. Rails会自<span style="font-family:STHeiti;">动加入相关的调用</span>.  
Rails关于文件名的思<span style="font-family:STHeiti;">维逻辑实例</span>:  
如果一个class名<span style="font-family:STHeiti;">为</span>:LineItem  
ralis将推出:  
1.此class<span style="font-family:STHeiti;">对应的数据库表格名为</span>line_items.  
2.此class<span style="font-family:STHeiti;">对应的文件名为</span>line_item.rb  
&#8230;.

<span style="font-family:STHeiti;">创建</span>model下的controller  
ruby script/generate controller Admin::Book action1 action2 &#8230;

使用debug() helper method

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Ruby on Rails项目文件目录结构和环境设置][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/107