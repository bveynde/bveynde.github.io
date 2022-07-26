---
title: Update if bigger
description: update a row if the new value is bigger than the current
date: 2022-07-19T10:27:44.453Z
preview: ""
draft: true
tags:
  - mysql
categories:
  - mysql
slug: update-bigger
---

## Issue
 * ...

## Example
```mysql
INSERT INTO CONTENT (content_id, version, description)
VALUES ('123', '1', 'This is an example')
ON DUPLICATE KEY
UPDATE version=
    CASE WHEN VALUES(version) > version THEN VALUES(version) ELSE version END,
description=
    CASE WHEN VALUES(version) > version THEN VALUES(description) ELSE description END
```

## Ref
 * [MySQL update if value is greater than current value](https://stackoverflow.com/questions/44380059/mysql-update-if-value-is-greater-than-current-value)
