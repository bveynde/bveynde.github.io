---
title: Hugo Debug
description: jsonify with these options gives me much more readable output than the printf
  function
date: 2022-07-15T14:05:59.498Z
preview: ""
draft: true
tags:
  - hugo
  - debug
categories:
  - hugo
slug: hugo-debug
---


## Old
```
{{ printf "%#v" . }}
```
*todo: add outut of both printf as jsonify*

## new
```
<pre>{{- jsonify (dict "prefix" " " "indent" "  ") . -}}</pre>
```

## Ref
 * [https://gohugo.io/templates/template-debugging/](https://gohugo.io/templates/template-debugging/)
 * [https://discourse.gohugo.io/t/not-understanding-debugging-need-more-clarity-on-variable-data/24252](https://discourse.gohugo.io/t/not-understanding-debugging-need-more-clarity-on-variable-data/24252)
 * [https://github.com/kaushalmodi/hugo-debugprint](https://github.com/kaushalmodi/hugo-debugprint)
