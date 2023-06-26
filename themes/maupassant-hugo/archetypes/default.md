---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
categories:
  - {{replace .Name "-*" ""}}
---

[TOC]

