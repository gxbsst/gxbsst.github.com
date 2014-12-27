---
layout: post
title: "Postgresql 分组查询"
date: 2014-12-27 14:47:01 +0800
comments: true
categories: ['postgresql']
---

### 数据
最近有一个项目，有一个表数据结构如下

name | description | technique_id | references_count
------------ | ------------- | ------------
name_1 | description 1  | 1 | 4
name_2 | description 2 |  2 | 5
name_1 | description 1  | 3 | 0
name_2 | description 2 |  1 | 2
name_1 | description 1  | 2 | 4
name_2 | description 2 |  3 | 3
name_2 | description 2 |  1 | 1
name_1 | description 1  | 2 | 2
name_2 | description 2 |  3 | 2

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

http://thehobt.blogspot.jp/2009/02/rownumber-rank-and-denserank.html
