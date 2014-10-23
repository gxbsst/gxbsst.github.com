---
title: PHP防mysql注入有用的函数mysql_real_escape_string()
author: gxbsst
layout: post
permalink: /archives/171
post_views_count:
  - 116
views:
  - 53
categories:
  - PHP
---
<pre lang="mysql">$sql = “select count(*) as ctr  from users where 
  username='foo' and password='' or '1'='1' limit 1”;

</pre>

以上语句总是返回1。。。怎麽辦？對or &#8217;1&#8242;=&#8217;1&#8242;轉義，就用以下函數  
mysql\_real\_escape_string()

<pre lang="php"><?php
$okay = 0;
$username = $_POST['user'];
$pw = $_POST['pw'];

$sql = "select count(*) as ctr from users where 
username='".mysql_real_escape_string($username)."' 
and password='". mysql_real_escape_string($pw)."' limit 1"; 

$result = mysql_query($sql);

while ($data = mysql_fetch_object($result)){
if ($data->ctr == 1){
//they're okay to enter the application!
$okay = 1;
}
}

if ($okay){
$_SESSION['loginokay'] = true;
header(“index.php”);
}else{
header(“login.php”);
}
?>

</pre>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [PHP防mysql注入有用的函数mysql\_real\_escape_string()][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/171