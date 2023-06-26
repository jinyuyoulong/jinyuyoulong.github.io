---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
toc: true
images:
categories:
  - {{replace .Name "-*" ""}}
tags: 
  - untagged
---

