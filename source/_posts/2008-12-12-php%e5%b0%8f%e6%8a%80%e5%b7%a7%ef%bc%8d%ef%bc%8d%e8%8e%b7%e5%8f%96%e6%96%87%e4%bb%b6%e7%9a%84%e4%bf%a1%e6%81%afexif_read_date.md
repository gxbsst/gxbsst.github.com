---
title: PHP小技巧－－获取文件的信息(exif_read_date ()
author: gxbsst
layout: post
permalink: /archives/223
post_views_count:
  - 177
views:
  - 118
categories:
  - PHP
---
<pre lang="php">$sourceImage = 'images/baby.jpg'; 
$exif_data = exif_read_data( $sourceImage );
echo '<pre>';
print_r($exif_data); 
echo '</pre>


<p>
  '; 
</p>


<p>
  显示
</p>


<pre lang="php">

Array
(
    [FileName] => baby.jpg
    [FileDateTime] => 1228665226
    [FileSize] => 20161
    [FileType] => 2
    [MimeType] => image/jpeg
    [SectionsFound] => APP12
    [COMPUTED] => Array
        (
            [html] => width=“204” height=“225”
            [Height] => 225
            [Width] => 204
            [IsColor] => 1
        )

    [Company] => Ducky
    [Info] => 
)

</pre>


<p>
  转载请注明：<a href="http://www.weixuhong.com">韦旭红的点点滴滴</a> &raquo; <a href="http://www.weixuhong.com/archives/223">PHP小技巧－－获取文件的信息(exif_read_date ()</a>
</p>