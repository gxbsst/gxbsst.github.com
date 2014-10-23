---
title: 关于Yii的AR（MANY-MANY)的问题
author: gxbsst
layout: post
permalink: /archives/253
post_views_count:
  - 128
views:
  - 31
categories:
  - PHP
---
Yii的AtiveRecord中的MANY-MANY一直是我困惑的问题。需要做这样设置。

**表的命名**  
假设我的表是这样命名:products_categories  
表字段:

<pre lang="bash">+-------------+---------+------+-----+---------+----------------+
| Field       | Type    | Null | Key | Default | Extra          |
+-------------+---------+------+-----+---------+----------------+
| product_id  | int(11) | NO   |     | 0       |                |
| category_id | int(11) | NO   |     | 0       |                |
| id          | int(11) | NO   | PRI | NULL    | auto_increment |
+-------------+---------+------+-----+---------+----------------+
</pre>

**model设置**

<pre lang="php">public function relations()
	{
		return array(
			'images' => array(self::HAS_MANY, 'Image', 'product_id'),
			'brand' => array(self::BELONGS_TO, 'Brand', 'brand_id'),
			'categories' => array(self::MANY_MANY, 'Category','products_categories(product_id , category_id)' )
			);
	}
</pre>

<p style="color:red">
  *如果你在product模型里面设置这个关系，表(table)命名一定要是:products_categories, 不然SQL语气会出错。<br /> *还有一个问题我不知道是不是Yii本身的Bug，我这里用categories命名的时候，我这样查找，竟然找不到！
</p>

<pre lang="php">$products = Product::model()->with('categories')->findAll("id = 227",array("order" => " name DESC"));
</pre>

<p style="color:red">
  我把categories => cat, (就是用另外的单词代替上面的categories）就可以了，具体是什么我还没有验证！
</p>

&#8211;EOF&#8211;

转载请注明：[韦旭红的点点滴滴][1] &raquo; [关于Yii的AR（MANY-MANY)的问题][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/253