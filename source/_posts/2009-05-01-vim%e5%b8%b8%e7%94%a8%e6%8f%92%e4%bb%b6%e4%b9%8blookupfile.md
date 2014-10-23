---
title: Vim常用插件之lookupfile
author: gxbsst
layout: post
permalink: /archives/249
post_views_count:
  - 164
views:
  - 143
categories:
  - Linux/Unix
---
VIM是一款强大的编辑器，它可以做很多事情，但是如果没有插件的支持，就会显得有写单调，但是配置好之后，绝对不输给任何编辑器，当然还有Emacs，也是很强大的编辑器之一，今后我会把我VIM配置的plubin列出来，以备忘，虽然我已经把它作为一个小的项目放在SVN里，今天介绍lookupfile。

lookupfile是通过输入关键字，就可以找到文件的插件，如同TextMate，目录下的通过关键字找文件。 

需要:ctags, genutils  
参考: http://easwy.com/blog/archives/advanced-vim-skills-lookupfile-plugin/ 

安装: ctags  
Linux 

<pre lang="bash">sudo apt-get install ctags 
</pre>

Mac 

<pre lang="bash">sudo port install ctags *我在mac下面编译，但是功能不如port安装的完全，所以在mac，要用port安装. 
</pre>

生成tags文件 

<pre lang="bash">ctags -R ./* (这一句将会会在当前目录生成一个tags的文件，以后vim,需要用到它. 
</pre>

安装：genutils，lookupfile  
genutils可以到: http://www.vim.org/scripts/script.php?script_id=197  
lookupfile可以到: http://www.vim.org/scripts/script.php?script_id=1581 

* 将文件下载到～/.vim目录下，然后解压就可以. 

配置VIM 

<pre lang="bash">:let g:LookupFile_TagExpr = '"./filenametags"' 
*其中filenametags就是刚才ctags生成的tags, 但是为了方面，我们在~/.vimrc添加这一行: (let g:LookupFile_TagExpr = '"./filenametags"') 
</pre>

接下来你就可以看到VIM的神奇了：  
：LookupFile 或者F5,就能打开lookupfile  
看图：  
![][1]  
真的很棒！

BTW,当然我这里所涉及的内容，前提条件是你要对*Nix系统要有一定的认识. 

&#8211;EOF&#8211;

转载请注明：[韦旭红的点点滴滴][2] &raquo; [Vim常用插件之lookupfile][3]

 [1]: http://b16.photo.store.qq.com/http_imgload.cgi?/rurl4_b=dff7d683dafddbcd0fa941ad9220442a41ac128db8e0d6bf653ae21f1d5617c1656752b9d2fb61bb084e687fd628d12065fc29b9433ecb651741bd7368ecf43e7e55d550118949967ba15a265b7d5c2a77dc23f3
 [2]: http://www.weixuhong.com
 [3]: http://www.weixuhong.com/archives/249