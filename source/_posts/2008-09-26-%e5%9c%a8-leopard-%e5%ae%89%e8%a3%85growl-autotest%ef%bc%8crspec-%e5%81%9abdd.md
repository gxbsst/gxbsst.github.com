---
title: 在 Leopard 安装Growl, Autotest，Rspec 做BDD
author: gxbsst
layout: post
permalink: /archives/188
post_views_count:
  - 121
views:
  - 32
categories:
  - 心情随写
---
1. 设置.autotest ( 需要安装以下gem)

<pre lang="shell">sudo gem install rspec  
   sudo gem install ZenTest  
   sudo gem install redgreen  

</pre>

vim ~/.autotest就可以编辑文件

<pre lang="ruby">require 'autotest/redgreen'  
  
module Autotest::Growl  
  def self.growl title, msg, img, pri=0, stick=“”  
    system “growlnotify -n autotest --image #{img} -p #{pri} -m #{ msg.inspect} #{title} #{stick}”  
  end  
  
  Autotest.add_hook :ran_command do |autotest|  
    filtered = autotest.results.grep(/d+s.*examples?/)  
    output = filtered.empty? ? “” : filtered.last.slice(/(d+)s.*examples?,s(d+)s.*failures?(?:,s(d+)s.*pending)?/)  
    if output =~ /[1-9]sfailures?/  
      growl “Test Results”, “#{output}”, “~/Library/autotest/rails_fail.png”  
    elsif output =~ /pending/  
      growl “Test Results”, “#{output}”, “~/Library/autotest/rails_pending.png”  
    else  
      growl “Test Results”, “#{output}”, “~/Library/autotest/rails_ok.png”  
    end  
  end  
      
end  
  
Autotest.add_hook :initialize do |at|  
    %w{.svn .hg .git vendor}.each {|exception| at.add_exception(exception)}  
end  

</pre>

2. 配置Growl(http://growl.info/)

*前提是要安装Growl

转载请注明：[韦旭红的点点滴滴][1] &raquo; [在 Leopard 安装Growl, Autotest，Rspec 做BDD][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/188