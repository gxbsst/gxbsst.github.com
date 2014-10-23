---
title: ruby on rails 环境的安装步骤
author: gxbsst
layout: post
permalink: /archives/73
post_views_count:
  - 109
views:
  - 46
categories:
  - Ruby/Ruby on Rails
---
Then run, apt-get update && apt-get upgrade

\# Configure SSH &#8212; You can just SSH in to do the Install from here&#8230;  
apt-get install openssh-server

\# Configure the Base System along with Trac/SVN  
apt-get install lynx autossh screen curl postfix tree  
xtightvncviewer module-assistant build-essential fakeroot  
dh-make debconf libstdc++5 gcc-3.3-base trac svnmailer debfoster 

aptitude install -y ruby ruby-dev ri rdoc irb ruby-examples  
libdbm-ruby libgdbm-ruby libopenssl-ruby libreadline-ruby  
rubygems

sudo gem update &#8211;system  
sudo gem install deprec &#8211;include-dependencies  
sudo gem install rails &#8211;include-dependencies  
sudo gem install termios

转载请注明：[韦旭红的点点滴滴][1] &raquo; [ruby on rails 环境的安装步骤][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/73