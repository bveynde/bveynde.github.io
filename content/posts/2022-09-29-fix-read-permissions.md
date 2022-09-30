---
title: Fix Read Permissions
description: We could not read all backup files from another user/server
date: 2022-07-19T10:27:44.453Z
preview: ""
draft: false
tags:
  - bash
categories:
  - scripting
slug: fix-read-permissions
---

## Issue
 * We could not read all backup files from another user/server
 * chmod -R a+r . fixed it, but was to slow
 * The current solution looks only at the most re 

## Example
```bash
# loop trough each dir + find the last sub-dir + chmod o+r on that sub-dir ...
for d in /nfs/backups/*/ ; do ls -d $d* | tail -1 | xargs chmod -R o+r  ; done 2>/dev/null
```

## Ref
 * [chmod(1) - Linux man page](https://linux.die.net/man/1/chmod)
