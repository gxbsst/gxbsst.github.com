---
title: Ruby 读取目录（Diretories)，文件(files), 网页的几个方法小结
author: gxbsst
layout: post
permalink: /archives/199
post_views_count:
  - 164
views:
  - 81
categories:
  - Ruby/Ruby on Rails
---
* 因为经常在console下面工作，操作文件的命令都还可以，但是想想用程式来操作，那也是更有意思，特别是在shell程序的时候&#8230;  
\* 熟悉\*inx命令的人，相信对这些ruby的方法会很熟悉的

1. 操作目录（Directories）  
A. 创建

<pre lang="ruby">Dir.chdir( “/Users/weston” )  #进入目录
home =Dir.pwd # => “/Users/weston/” * 显示目录
Dir.mkdir( “/Users/weston/” )  ＃创建目录，和*nix命令一样吧
Dir.rmdir( “/Users/weston/test” ) # 删除目录
Dir.mkdir( “/Users/weston/test”,755 ) #常见目录，设置权限
</pre>

B.查看

<pre lang="ruby">d = Dir.entries( “/Users/weston” ).each { |e| puts e } #=> Array

＃ 当然会有些隐藏文件，很方便的用数组操作，不显示隐藏文件

d2 = d.delete_if{ |e| e=~ /^..*/} #=>这样出来的就是不包含隐藏文件了

</pre>

C. 打开目录

<pre lang="ruby">dir = Dir.open( “/Users/weston” ) # => #&lt;Dir:0x1cd784> 
dir.path # => “/Users/weston” 
dir.tell # => “.” 
dir.read # => 1
dir.tell # => “..” 
dir.rewind # => rewind to beginning 
dir.each { |e| puts e } # puts each entry in dir 
dir.close # => close stream 
</pre>

2. 文件（ Files ）  
A. 创建

<pre lang="ruby">file = File.new( “file.rb”, “w” ) # => #&lt;File:file.rb> 
* 其中的w是表示可以写，还有很多模式：r, r+, w, w+, a, a+,b
</pre>

B. 打开文件

<pre lang="ruby">file = File.open( “sonnet_129.txt” ) 
file.each { |line| print “#{file.lineno}. ”, line } 
file.close

#lineno 是行号
</pre>

C. 删除或重命名文件

<pre lang="ruby">File.new( “books.txt”, “w” ) 
File.rename( “books.txt”, “chaps.txt” ) 
File.delete( “chaps.txt” ) 

</pre>

3. 操作URI

<pre lang="ruby">require 'open-uri' 
url = “http://www.google.com/search?q=ruby” 
open(url) { |page| page_content = page.read()
links = page_content.scan(/&lt;a class=l.*?href="(.*?)"/).flatten 
links.each {|link| puts link} 
}
</pre>

4. File Inquiries

<pre lang="ruby">File::open(“file.rb”) if File::exists?( “file.rb” ) 
File.file?( “sonnet29.txt” ) # => true 
# try it with a directory 
File::directory?( “/usr/local/bin” ) # => true 

＃ 是否是目录
# try it with a file...oops 
File::directory?( “file.rb” ) # => false 

＃ 文件操作权限
File.readable?( “sonnet_119.txt” ) # => true 
File.writable?( “sonnet_119.txt” ) # => true 
File.executable?( “sonnet_119.txt” ) # => false 
system(“touch chap.txt”) # Create a zero-length file with a system command 
File.zero?( “chap.txt” ) # => true 


＃ 文件大小
# Get its size in bytes withsize? orsize: 
File.size?( “sonnet_129.txt” ) # => 594 
File.size( “sonnet_129.txt” ) # => 594 

# 文件类型
# Finally, inquire about the type of a file withftype: 
File::ftype( “file.rb” ) # => “file” 
＃ 创建，修改时间
File::ctime( “file.rb” ) # => Wed Nov 08 10:06:37 -0700 2006 
File::mtime( “file.rb” ) # => Wed Nov 08 10:44:44 -0700 2006 
File::atime( “file.rb” ) # => Wed Nov 08 10:45:01 -0700 2006 


</pre>

5. Changing File Modes and Owner

<pre lang="ruby">file = File.new( “books.txt”, “w” ) 
file.chmod( 0755 ) 


or: 
file = File.new( “books.txt”, “w” ).chmod(0755 ) 
system “ls -l books.txt” # => -rwxr-xr-x     1 mikejfz  mikejfz     0 Nov  8 22:13 
books.txt
</pre>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Ruby 读取目录（Diretories)，文件(files), 网页的几个方法小结][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/199