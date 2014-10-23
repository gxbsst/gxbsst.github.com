---
title: SVN 自动发布（SVN Auto Commit)
author: gxbsst
layout: post
permalink: /archives/261
post_views_count:
  - 158
views:
  - 87
categories:
  - Linux/Unix
---
<div class="wp_syntax">
  <div class="code">
    <pre class="bash">
#!/bin/bash
# Run commit every second.
# Why? Cron can't do that.

# Example:
# ./commit [svn url] [local svn path]

while [ true ]; do
data=`date`
message="*Auto-message*"
stat=`svn status $2`
if [[ $stat != '' ]]; then
delete_files=`svn status $2 |grep -e "^!"|cut -d" " -f7`
if [[ $delete_files != '' ]]; then
svn delete `svn status $2 |grep -e "^!"|cut -d" " -f7`>/dev/null 2>/dev/null # Add new files if there are any
svn commit --non-interactive -m "$message (delete)" $2 >/dev/null 2>>commit_log # Finaly commit
echo $delete_files $data
fi
add_files=`svn status $2 |grep -e "^?"|cut -d" " -f7`
if [[ $add_files != '' ]]; then
svn add $add_files >/dev/null 2>/dev/null # Add new files if there are any
svn commit --non-interactive -m "$message (add)" $2 >/dev/null 2>>commit_log # Finaly commit
echo $delete_files $data
fi
svn checkout $1 $2 >/dev/null 2>>/dev/null # Checkout
svn commit --non-interactive -m $message $2 >/dev/null 2>>commit_log # Finaly commit
echo $stat $data
fi
sleep 1
done
</pre>
  </div>
</div>

* 将以上脚本放在要自动发布的目录下  
* 配置ctrontab让其自动发布

转载请注明：[韦旭红的点点滴滴][1] &raquo; [SVN 自动发布（SVN Auto Commit)][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/261