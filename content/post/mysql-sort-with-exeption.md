---
author: Bart Van Eynde
title: MySQL - Sort with an axeption
date: 2022-06-08
description: sort your select, keep an item on top
categories: tipsntricks
tags:
  - mysql
---

## Situation
This query must give the data for a dropdown list in a html form.

## Requirements
 * If nothing is selected, "9999 - tbd", must be the first choise
 * make sure the current name is in the list, even if it is inactive today
 * sort names alphabeticly 


## test data
```mysql
CREATE TABLE temp.D_id_name as
select 8962 `id`, 'Ollie Sears' `name`, 'Y' `active`
union all select 3710 , 'Humayra Hall', 'N' 
union all select 9489 , 'Ember Salas', 'Y' 
union all select 370 , 'Bella-Rose Quintana', 'N' 
union all select 4458 , 'Arlene Goff', 'Y' 
union all select 497 , 'Sharmin Naylor', 'N' 
union all select 8971 , 'Ansh Davenport', 'Y' 
union all select 4295 , 'Hajra Wilson', 'N' 
union all select 3091 , 'Jo Howarth', 'Y' 
union all select 2281 , 'Ana Hickman', 'N' 
;
```

## Query
```mysql
SELECT * FROM ( 
    ( 
        SELECT 9999 `id`, 'tbd' `name` 
    ) UNION ALL ( 
        SELECT id , name FROM temp.D_id_name WHERE active='Y' OR id=4295 
    ) 
) a 
ORDER BY `name`!='tbd',`name` ASC 
;
```
### Result
```
+------+----------------+
| id   | name           |
+------+----------------+
| 9999 | tbd            |
| 8971 | Ansh Davenport |
| 4458 | Arlene Goff    |
| 9489 | Ember Salas    |
| 4295 | Hajra Wilson   |
| 3091 | Jo Howarth     |
| 8962 | Ollie Sears    |
+------+----------------+
```

or...
This was my first try with info from the internet, but the above syntax is more elegant.
```
ORDER BY `id`=9999 desc,`name` ASC 
```