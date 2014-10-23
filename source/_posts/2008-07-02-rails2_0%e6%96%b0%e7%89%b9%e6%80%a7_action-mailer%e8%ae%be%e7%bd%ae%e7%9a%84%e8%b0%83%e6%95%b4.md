---
title: Rails2_0新特性_Action Mailer设置的调整
author: gxbsst
layout: post
permalink: /archives/141
post_views_count:
  - 129
views:
  - 30
categories:
  - Ruby/Ruby on Rails
---
用于<span style="font-family:STHeiti;">邮件服务的</span>Action mailer控件在原基<span style="font-family:STHeiti;">础上做了一些更改。特别是对于使用</span>edge rails的程序<span style="font-family:STHeiti;">员来说，这个更新尤其重要。先前的</span>ActionMailer::base.server\_settings被 ActionMailer::Base.smtp\_settings取代，不<span style="font-family:STHeiti;">过这个变化只停留在表面（名称的变化），而实质的语法仍被保留不变：</span>

<p style="text-indent:40pt;">
  <span style="color:#92d230;background-color:#4280d2;">ActionMailer::Base.delivery_method = :smtp<br /> ActionMailer::Base.smtp_settings = {<br /> :address => “smtp.mymailserver.com”,<br /> :authentication => :login,<br /> :user_name => “me”,<br /> :password => “password”<br /> }</span>
</p>

在Rails 的 1-2-stable branch 下server_settings的用法已<span style="font-family:STHeiti;">经被删减。同时，</span> edge版本 中的所有命名也已被完全修改，相<span style="font-family:STHeiti;">对的，读者也需要更新自己的项目代码。</span>

而且，<span style="font-family:STHeiti;">这个升级还为我们带来两个新的扩展：为</span>ActionMailer::Base.sendmail_settings <span style="font-family:STHeiti;">设置可运行</span> sendmail 的位置以及其命令行参数 （如果你在使用sendmail)

<span style="background-color:#b0b0b0;">ActionMailer::Base.delivery_method = :sendmail<br /> ActionMailer::Base.sendmail_settings = {<br /> :location => &#8216;/usr/sbin/sendmail&#8217;,<br /> :arguments => &#8216;-i -t&#8217;</span><span style="color:#b0b0b0;background-color:#b0b0b0;"><br /> }</span>  
要<span style="font-family:STHeiti;">查看更多的选择可以参考</span> ActionMailer::Base API

原文作者是 Ryan Daigle, <span style="font-family:STHeiti;">请访问他的博客</span>  
本片<span style="font-family:STHeiti;">译文的原文地址：</span>

http://ryandaigle.com/articles/2007/1/31/what-s-new-in-edge-rails-actionmailer-base-server_settings-deprecated

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Rails2\_0新特性\_Action Mailer设置的调整][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/141