---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
description: 
weight: 999
authors:
  - ra
resources:
  - src: foo.jpg
    title: Foo
    params:
      author:
      source:
---
