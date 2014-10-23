---
title: 'Nested set model: Copy SubTree'
author: gxbsst
layout: post
permalink: /archives/402
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 196
views:
  - 98
categories:
  - PHP
---
要点：

1. 撑宽目标node的宽度 shift R && L Values

<pre lang="php">$first = $parent_manual['node']['l']+1; //The dst node l value

$delta  = $current_manual['rgt'] - $current_manual['lft']+1;

mysql_query('START TRANSACTION');
  $result_a = mysql_query("UPDATE ".$thandle['table']." SET ".$thandle['lvalname']."=".$thandle['lvalname']."+$delta WHERE ".$thandle['lvalname'].">=$first ");
  $result_b = mysql_query("UPDATE ".$thandle['table']." SET ".$thandle['rvalname']."=".$thandle['rvalname']."+$delta WHERE ".$thandle['rvalname'].">=$first ");
	/*IF UPDATE IS SUCCESS ,THEN DO COMMIT*/
	if ($result_a &#038;&#038; $result_b) {
		mysql_query('COMMIT');
	} else {
		mysql_query('ROLLBACK');
	}

</pre>

2. 复制的操作

<pre lang="php">$delta  = $parent_manual['node']['l'] - $current_manual['lft'] + 1;

	foreach ($tree as  $manual) {
	$manual['description'] = '';
	$manual['lft'] += $delta;
	$manual['rgt'] += $delta ;
	$manual['root_id'] = $root_id;
	copy_one_item($manual, $root_id, $thandle);
}

</pre>

* 其实最重要的就是$first和$delta的计算方法.

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Nested set model: Copy SubTree][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/402