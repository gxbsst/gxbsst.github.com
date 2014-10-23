---
title: 'HowTo: install ngnix on ubuntu'
author: gxbsst
layout: post
permalink: /archives/189
post_views_count:
  - 140
views:
  - 58
categories:
  - 技术感想
---
<pre lang="shell">1.  apt-get install libpcre3-dev
2.  sudo apt-get install zlib1g-dev
3. ./configure &#038;&#038; make &#038;&#038; make install
</pre>

prealpha的ngnix的配置文件:

<pre lang="c">user deploy;
worker_processes  1;
error_log  logs/error.log debug;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;
pid        logs/nginx.pid;
events {
    worker_connections  1024;
}
http {
  include       conf/mime.types;
  default_type  application/octet-stream;
  sendfile        on;
  #tcp_nopush     on;
  keepalive_timeout  65;
  tcp_nodelay        on;
  gzip  on;
  gzip_min_length  1100;
  gzip_buffers     4 8k;
  gzip_types       text/plain;
  upstream mongrel {
    server 127.0.0.1:8000;
    server 127.0.0.1:8001;
    server 127.0.0.1:8002;
  }
  upstream apache {
    server 127.0.0.1:88;
  }
  server {
    listen       80;
    server_name  prealpha.red.com;
    root /var/www/prealpha/store/public;
    index  index.html index.htm;
    location /faq {
        proxy_redirect http://$http_host/faq/ http://$http_host/faq/;
    }
    location /faq/ {
        proxy_pass http://apache;
    }
    location / {
      proxy_set_header  X-Real-IP  $remote_addr;
      proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header Host $http_host;
#      auth_basic           "/";
#      auth_basic_user_file  conf/htpasswd;
      if (-f $request_filename/index.html) {
        rewrite (.*) $1/index.html break;
      }
      if (-f $request_filename.html) {
        rewrite (.*) $1.html break;
      }
      if (!-f $request_filename) {
        proxy_pass http://mongrel;
        break;
      }
    }
  
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   html;
    }
  }
}

</pre>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [HowTo: install ngnix on ubuntu][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/189