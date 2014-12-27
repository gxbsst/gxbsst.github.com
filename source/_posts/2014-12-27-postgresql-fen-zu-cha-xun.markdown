---
layout: post
title: "Postgresql 分组查询"
date: 2014-12-27 14:47:01 +0800
comments: true
categories: ['postgresql']
---

### 数据
最近有一个项目，有一个表数据结构如下

<table>
<thead>
<tr>
  <td>name</td>
  <td>description</td>
  <td> technique_id </td>
  <td>references_count</td>
</tr>
</thead>
<tbody>
<tr>
  <td>name_1</td>
  <td>description</td>
  <td>1</td>
  <td>5</td>
</tr>

<tr>
  <td>name_2</td>
  <td>description</td>
  <td>2</td>
  <td>4</td>
</tr>

<tr>
  <td>name_3</td>
  <td>description</td>
  <td>3</td>
  <td>2</td>
</tr>

<tr>
  <td>name_1</td>
  <td>description</td>
  <td>1</td>
  <td>5</td>
</tr>

<tr>
  <td>name_2</td>
  <td>description</td>
  <td>2</td>
  <td>4</td>
</tr>

<tr>
  <td>name_3</td>
  <td>description</td>
  <td>3</td>
  <td>2</td>
</tr>

<tr>
  <td>name_1</td>
  <td>description</td>
  <td>1</td>
  <td>5</td>
</tr>

<tr>
  <td>name_2</td>
  <td>description</td>
  <td>2</td>
  <td>4</td>
</tr>

<tr>
  <td>name_3</td>
  <td>description</td>
  <td>3</td>
  <td>2</td>
</tr>


</tbody>
</table>


### 需求
**现在需要通过一条sql语句， 通过几个 technique_id 查找， 每个technique_id 查找3条， 并且按照references_count降序**

### 实现

``` sql
SELECT * from (
  SELECT *, RANK() OVER (PARTITION BY technique_id ORDER BY reference_count DESC) AS RP FROM gauges
) 
G WHERE G.rp <= 3"
```


### 参考

[http://thehobt.blogspot.jp/2009/02/rownumber-rank-and-denserank.html](http://thehobt.blogspot.jp/2009/02/rownumber-rank-and-denserank.html)
