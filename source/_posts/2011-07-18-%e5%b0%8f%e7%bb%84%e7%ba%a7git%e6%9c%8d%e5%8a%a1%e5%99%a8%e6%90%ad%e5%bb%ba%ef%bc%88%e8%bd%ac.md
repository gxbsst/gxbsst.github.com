---
title: 小组级git服务器搭建（转)
author: gxbsst
layout: post
permalink: /archives/541
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 291
views:
  - 202
categories:
  - Linux/Unix
---
来自：http://blog.prosight.me/index.php/2009/11/485

如果使用git的人数较少，可以使用下面的步骤快速部署一个git服务器环境。  
1. 生成 SSH 公钥  
每个需要使用git服务器的工程师，自己需要生成一个ssh公钥  
进入自己的~/.ssh目录，看有没有用 文件名 和 文件名.pub 来命名的一对文件，这个 文件名 通常是 id\_dsa 或者 id\_rsa。 .pub 文件是公钥，另一个文件是密钥。假如没有这些文件（或者干脆连 .ssh 目录都没有），你可以用 ssh-keygen 的程序来建立它们，该程序在 Linux/Mac 系统由 SSH 包提供， 在 Windows 上则包含在 MSysGit 包里:

<pre lang="c">$ ssh-keygen 
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/schacon/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/schacon/.ssh/id_rsa.
Your public key has been saved in /Users/schacon/.ssh/id_rsa.pub.
The key fingerprint is:
43:c5:5b:5f:b1:f1:50:43:ad:20:a6:92:6a:1f:9a:3a schacon@agadorlaptop.local
</pre>

它先要求你确认保存公钥的位置（.ssh/id_rsa），然后它会让你重复一个密码两次，如果不想在使用公钥的时候输入密码，可以留空。  
现在，所有做过这一步的用户都得把它们的公钥给你或者 Git 服务器的管理者（假设 SSH 服务被设定为使用公钥机制）。他们只需要复制 .pub 文件的内容然后 e-

<pre lang="c">$ cat ~/.ssh/id_rsa.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU
GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3
Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA
t3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En
mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx
NrRFi9wrf+M7Q== schacon@agadorlaptop.local
</pre>

2. 架设服务器  
首先，创建一个 ‘git’ 用户并为其创建一个 .ssh 目录，在用户主目录下:

<pre lang="c">$ sudo adduser git
$ su git
$ cd
$ mkdir .ssh
</pre>

接下来，把开发者的 SSH 公钥添加到这个用户的 authorized\_keys 文件中。假设你通过 e-mail 收到了几个公钥并存到了临时文件里。只要把它们加入 authorized\_keys 文件

<pre lang="c">$ cat /tmp/id_rsa.john.pub >> ~/.ssh/authorized_keys
$ cat /tmp/id_rsa.josie.pub >> ~/.ssh/authorized_keys
$ cat /tmp/id_rsa.jessica.pub >> ~/.ssh/authorized_keys
</pre>

现在可以使用 –bare 选项运行 git init 来设定一个空仓库，这会初始化一个不包含工作目录的仓库。

<pre lang="c">$ cd /opt/git
$ mkdir project.git
$ cd project.git
$ git --bare init
</pre>

这时，开发人员就可以把它加为远程仓库，推送一个分支，从而把第一个版本的工程上传到仓库里了。值得注意的是，每次添加一个新项目都需要通过 shell 登入主机并创建一个纯仓库。我们不妨以 gitserver 作为 git 用户和仓库所在的主机名。如果你在网络内部运行该主机，并且在 DNS 中设定 gitserver 指向该主机，那么以下这些命令都是可用的：

\# 在一个工程师的电脑上

<pre lang="c">$ cd myproject
$ git init
$ git add .
$ git commit -m 'initial commit'
$ git remote add origin git@gitserver:/opt/git/project.git
$ git push origin master
</pre>

这样，其他人的克隆和推送也一样变得很简单：

<pre lang="c">$ git clone git@gitserver:/opt/git/project.git
$ vim README
$ git commit -am 'fix for the README file'
$ git push origin master
</pre>

用这个方法可以很快捷的为少数几个开发者架设一个可读写的 Git 服务。  
作为一个额外的防范措施，你可以用 Git 自带的 git-shell 简单工具来把 git 用户的活动限制在仅与 Git 相关。把它设为 git 用户登入的 shell，那么该用户就不能拥有主机正常的 shell 访问权。为了实现这一点，需要指明用户的登入shell 是 git-shell ，而不是 bash 或者 csh。你可能得编辑 /etc/passwd 文件

<pre lang="c">$ sudo vim /etc/passwd
</pre>

在文件末尾，你应该能找到类似这样的行：

<pre lang="c">git:x:1000:1000::/home/git:/bin/sh
</pre>

把 bin/sh 改为 /usr/bin/git-shell （或者用 which git-shell 查看它的位置）。该行修改后的样子如下：

git:x:1000:1000::/home/git:/usr/bin/git-shell  
现在 git 用户只能用 SSH 连接来推送和获取 Git 仓库，而不能直接使用主机 shell。尝试登录的话，你会看到下面这样的拒绝信息：

<pre lang="c">$ ssh git@gitserver
</pre>

fatal: What do you think I am? A shell? （你以为我是个啥？shell吗？)  
Connection to gitserver closed. （gitserver 连接已断开。）

转载请注明：[韦旭红的点点滴滴][1] &raquo; [小组级git服务器搭建（转)][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/541