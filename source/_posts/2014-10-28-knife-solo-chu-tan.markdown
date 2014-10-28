---
layout: post
title: "knife-solo 初探"
date: 2014-10-28 10:22:06 +0800
comments: true
categories: ['knife-solo', 'chef', 'vagrant']
---

#写在前面的话

做了多年的项目， 一直使用<a href="http://capistranorb.com" >capistrano</a>发布项目, 这个确实带来很大的便利。但是有点比较麻烦的地方，就是每次部署新的服务器，都像做苦力一样，去安装服务器的环境，后来了解到Chef和knife-solo, 其就可以达到类似capistrano所作的事情， 不过一个是一键发布项目，一个是一键安装服务器环境，好了，让我们开始吧！

# 准备工作

我们需要一台测试服务器，这个我们需要Vagrant帮我们实现。

## 安装vagrant

1. 先到这里下载Vagrant : https://www.vagrantup.com/downloads.html
> 注意： 旧的版本是通过gem install vagrant 安装

2. 安装box

``` bash
vagrant init hashicorp/precise32
```
> 到这里发现更多的box: http://vagrantcloud.com

3. 启动

``` bash
vagrant up
```
4. 配置ssh登录不需要密码

``` bash
vagrant ssh-config --host   服务器IP >> ~/.ssh/config
```
## 安装chef-solo

1. 安装chef 和 chef-solo

``` bash
gem install chef
gem install knife-solo
或者
bundle init
编辑Gemfile
添加: 
source "https://rubygems.org"
gem "knife-solo"
执行:
bundle install --path=vendor/bundle
```

2. 初始化knife-solo项目

``` bash
knife solo init chef-repo
cd chef-repo
git init
git commit -a -m "initial commit"
knife solo prepare ServerIP --bootstrap-version 11.12.0 # 如果这里不指定版本号， 会提示找不到文件的错误
```
``` bash
需要指定这个版本号 --bootstrap-version 11.12.0 # 如果这里不指定版本号， 会提示找不到文件的错误
wnloading Chef 12.0.0.alpha.2 for ubuntu...
downloading https://www.opscode.com/chef/metadata?v=12.0.0.alpha.2&prerelease=false&nightlies=false&p=ubuntu&pv=12.04&m=i686
  to file /tmp/install.sh.5074/metadata.txt
trying wget...
ERROR 404
Unable to retrieve a valid package!
Please file a bug report at http://tickets.opscode.com
Project: Chef
Component: Packages
Label: Omnibus
Version: 12.0.0.alpha.2
Please detail your operating system type, version and any other relevant details
Metadata URL: https://www.opscode.com/chef/metadata?v=12.0.0.alpha.2&prerelease=false&nightlies=false&p=ubuntu&pv=12.04&m=i686
```


# 通过Knife Solo 安装Nginx

1. 生成模板文件

``` bash
knife cookbook create nginx -o site-cookbooks
```

2. 编辑模板

``` ruby
site-cookbooks/nginx/recipes/default.rb
package "nginx" do
    action :install
end
service "nginx" do
    supports :status => true, :restart => true, :reload => true
    action [:enable, :start]
end
template "nginx.conf" do
    path "/etc/nginx/nginx.conf"
    source "nginx.conf.erb"
    owner "root"
    group "root"
    mode 0644
    notifies :reload , "service[nginx]"
end
```

``` 
user vagrant;  # 这里可以用nginx，但是需要新建这个用户
worker_processes    1;
error_log   /var/log/nginx/error.log;
pid /var/run/nginx.pid;
events {
    worker_connections 1024;
}
http {
    include /etc/nginx/mime.types;
    default_type application/octet-stream;
    server {
        listen <%= node['nginx']['port'] %>;
        server_name localhost;
        location / {
            root /usr/share/nginx/html;
            index index.html index.htm;
        }
    }
}
```



3. 在服务器上安装nginx

``` bash
knife solo cook SERVER_IP
```

# 参考

1. http://qiita.com/torufurukawa/items/e20bdb9791c49d00672e
2. http://gogojimmy.net/2013/06/01/Chef-Solo-Basic-with-Vagrant/
3. https://docs.vagrantup.com/v2/getting-started/index.html
4. http://vagrantcloud.com
