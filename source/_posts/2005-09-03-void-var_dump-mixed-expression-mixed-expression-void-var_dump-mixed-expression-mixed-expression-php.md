---
title: |
  void var_dump ( mixed expression [, mixed expression [, ...]] )
  void var_dump ( mixed expression [, mixed expression [, ...]] ) php&#8230;.
author: gxbsst
layout: post
permalink: /archives/173
post_views_count:
  - 189
views:
  - 35
categories:
  - PHP
---
void var_dump ( mixed expression [, mixed expression [, ...]] )

此函数显示关于一个或多个表达式的结构信息，包括表达式的类型与值。数组将递归展开值，通过缩进显示其结构。

提示: 为了防止程序直接将结果输出到浏览器，可以使用输出控制函数（output-control functions）来捕获此函数的输出，并把它们保存到一个例如 string 类型的变量中。

可以比较一下 var\_dump() 与 print\_r

<pre lang="php"><?php
$a = array (1, 2, array ("a", "b", "c"));
var_dump ($a);

/* 输出：
array(3) {
  [0]=>
  int(1)
  [1]=>
  int(2)
  [2]=>
  array(3) {
    [0]=>
    string(1) “a”
    [1]=>
    string(1) “b”
    [2]=>
    string(1) “c”
  }
}

*/

$b = 3.1;
$c = TRUE;
var_dump($b,$c);

/* 输出：
float(3.1)
bool(true)

*/
?>
</pre>

也可以参考 var_exprot (http://cn2.php.net/manual/en/function.var-export.php)

转载请注明：[韦旭红的点点滴滴][1] &raquo; [void var\_dump ( mixed expression [, mixed expression [, ...]] ) void var\_dump ( mixed expression [, mixed expression [, ...]] ) php&#8230;.][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/173