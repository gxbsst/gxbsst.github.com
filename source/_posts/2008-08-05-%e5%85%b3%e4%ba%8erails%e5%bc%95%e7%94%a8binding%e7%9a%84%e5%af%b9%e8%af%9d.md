---
title: 关于rails引用binding的对话
author: gxbsst
layout: post
permalink: /archives/161
post_views_count:
  - 106
views:
  - 45
categories:
  - Ruby/Ruby on Rails
---
* 以下是我同事Jerry的谈话介绍

鸡蛋黄(77883817) 19:29:17  
我说的简单了点，真正的 Rails 的代码会另外复制一个状态创造 binding 的 

鸡蛋黄(77883817) 19:29:44  
比如有个模板是 <%= @name %> 

鸡蛋黄(77883817) 19:30:09  
然后有个对象  
class People  
def initialize(name)  
@name = name  
end  
end 

鸡蛋黄(77883817) 19:30:29  
那么 People.new(“your name”).send(:binding) 就会得到一个 binding 对象 

鸡蛋黄(77883817) 19:30:51  
可以说这个对象就是保存了这个 people 实例的环境，自然包括了 @name 

微风(297749) 19:31:13  
binding是这个对象的context，可以这样理解？ 

鸡蛋黄(77883817) 19:31:15  
ERB.new(“<%= @name %>”).result( binding ) 能得到结果 

鸡蛋黄(77883817) 19:31:17  
可以 

鸡蛋黄(77883817) 19:31:35  
有了binding 

鸡蛋黄(77883817) 19:31:42  
甚至可以调用私有方法…… 

古月星辰(65009835) 19:31:44  
可以给action指定layout吗？ 

鸡蛋黄(77883817) 19:31:46  
有点不太干净哦？ 

鸡蛋黄(77883817) 19:31:58  
render :action => “action”, :layout => “abc 

* 1. 将实例的变量放到binding环境  
People.new(”your name“).send(:binding)  
* 2. 引用binding的环境的变量&#8230;  
ERB.new(”<%= @name %>“).result( binding )  
* 3. 甚至可以调用私有方法…… (如果People有私有方法，也可以调用)

转载请注明：[韦旭红的点点滴滴][1] &raquo; [关于rails引用binding的对话][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/161