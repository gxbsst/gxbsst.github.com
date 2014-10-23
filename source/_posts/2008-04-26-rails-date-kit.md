---
title: Rails Date Kit
author: gxbsst
layout: post
permalink: /archives/56
post_views_count:
  - 85
views:
  - 47
categories:
  - 心情随写
---
文章引用：http://www.methods.co.nz/rails\_date\_kit/rails\_date\_kit.html#toc1

Download

http://www.methods.co.nz/rails\_date\_kit/rails\_date\_kit_1.1.0.tar.gz

step by step:  
1.Setting application wide date display format

ActiveSupport::CoreExtensions::Date::Conversions::DATE_FORMATS.merge!(  
:default => &#8216;%d %b %Y&#8217;  
)

2.Inputting dates with the date_field helper and calendar control

#

Put calendar.js in ./public/javascripts.  
#

Put calendar.css in ./public/stylesheets.  
#

Put calendar\_prev.png and calendar\_next.png in ./public/images.  
#

Put date_helper.rb in ./app/helpers.  
#

In controllers that input dates (or in the application base controller ./app/controllers/application.rb) put:

helper :date

#

Put the following lines in your page headers:

<%= stylesheet\_link\_tag 'calendar' %>

<%= javascript\_include\_tag 'calendar' %>  
#

In templates with forms that input dates use the date_field helper. For example:

<%= date_field('person', 'birthday', :value => @person.birthday) %>

Note  
The date value is passed explicitly to ensure it&#8217;s formatted with the :default date format (see explanation in previous section).

3.Date Validation

Drop date_validator.rb into ./lib.

Require the validator in your models and add date validations. For example:

require\_dependency &#8216;date\_validator&#8217;

validates_dates :birthday,  
:from => &#8217;1 Jan 1930&#8242;,  
:to => Date.today,  
:allow_nil => true

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Rails Date Kit][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/56