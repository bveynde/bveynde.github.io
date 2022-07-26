---
title: created and updated date from tables
description: When was a Table Created and Last Updated
date: 2022-07-19T13:52:47.984Z
preview: ""
draft: true
tags:
  - mysql
  - date
categories:
  - mysql
---


## The Query
```mysql
SELECT  TABLE_SCHEMA
	, TABLE_NAME
	, CREATE_TIME
	, TIME_TO_SEC(timediff(NOW(),CREATE_TIME)) `Create_Sec_Ago` 
	, UPDATE_TIME
	, TIME_TO_SEC(timediff(NOW(),UPDATE_TIME)) `Update_Sec_Ago` 
FROM INFORMATION_SCHEMA.TABLES
WHERE table_schema = 'db_name'
	AND table_name LIKE 'table_prefix_%'
;
```

## Sample Output
```
+--------------+-------------------+---------------------+----------------+---------------------+----------------+
| TABLE_SCHEMA | TABLE_NAME        | CREATE_TIME         | Create_Sec_Ago | UPDATE_TIME         | Update_Sec_Ago |
+--------------+-------------------+---------------------+----------------+---------------------+----------------+
| Test         | table_prefix_OLD  | 2022-07-19 15:31:28 |           1616 | 2022-07-19 15:20:46 |           2258 |
| Test         | table_prefix      | 2022-07-19 15:31:28 |           1616 | 2022-07-19 15:31:28 |           1616 |
+--------------+-------------------+---------------------+----------------+---------------------+----------------+

```

## Ref
 * [StackOverflow - How to get the difference between two timestamps in seconds](https://stackoverflow.com/questions/3528219/how-to-get-the-difference-between-two-timestamps-in-seconds)