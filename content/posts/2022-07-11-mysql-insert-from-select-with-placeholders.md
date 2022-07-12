---
title: MySQL - Insert from Select with placeholders
description: When creating a monster joined table, is is sometimes faster to make a table
  with placeholders and afterwards fill it with update queries...
date: 2022-07-11
preview: ""
draft: false
tags:
  - mysql
categories:
  - tipsntricks
slug: mysql-insert-select-placeholders
keywords:
  - insert
  - mysql
  - "null"
  - placeholder
  - table
---
## Situation
When creating a monster joined table (a view was to slow), is is sometimes faster to make a table with placeholders and afterwards fill it with update queries...

## Requirements
 * Not a fixed table = less work when upstrean a new field is added
 * NULL placeholders, but with the correct structure 


## Query
```mysql
CREATE TABLE temp.test_cast_from_select as
SELECT 1 `id`
	, CAST( NULL AS VARCHAR(100) ) `v1`
	, CAST( NULL AS INT ) `v2`
	, CAST( NULL AS DATETIME ) `v3`
;
```
