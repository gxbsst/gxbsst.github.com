---
title: Block, Closures And Proc(块，闭包和Proc）的关系
author: gxbsst
layout: post
permalink: /archives/144
post_views_count:
  - 117
views:
  - 42
categories:
  - Ruby/Ruby on Rails
---
a = 1  
pr = Proc.new{ puts a }  
闭包可以用Proc来创建，参数是block&#8230;

This example shows a return failing because the context of its block no longer exists.  
def meth2(&b)  
b  
end  
*因为block是没有上下文(环境),如果你都没有在办公室这个环境，我当然不能叫你出办公室.  
但是闭包就不一样啊，闭包有自己的上下文，所以可以用这个以下方法  
* 补充： return 会返回值(true, false, nil,其他，后面的代码就补执行)，它的接受者是调用它的对象&#8230;接受者都没有，当然会出错&#8230;

*block只是代码块的匿名函数&#8230;或者说一个环境的一个配件&#8230;

<pre lang="ruby">def meth4
p = Proc.new { return 99 }
p.call
puts “Never get here”
end
meth4 → 99
</pre>

*p是一个proc创建的闭包，有自己的上下文（环境），所以可以return&#8230;

*block 是closure， 它能记住其被定义时的上下文， 并再调用时使用该上下文:

<pre lang="ruby">class Holder
  CONST = 100
  def call_block
    a = 101
    @a = 102
    @@a = 103
    yield
  end



end


class Creator
  CONST = 0
  def create_block
    a = 1
    @a = 2
    @@a = 3
    proc do   #=> return proc 
      puts “a = #{a}”
      puts “@a = #{@a}”
      puts “@@a = #{@@a}”
      puts yield
    end
  end
  
 end


block = Creator.new.create_block{“yield me”} #=> return a block 

Holder.new.call_block(&#038;block) #return the original context

a = 1
@a = 2
@@a = 3
yield me


</pre>

*3种方式将block转化成Proc对象

参考Programming ruby 第二版 P358

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Block, Closures And Proc(块，闭包和Proc）的关系][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/144