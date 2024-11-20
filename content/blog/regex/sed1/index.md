---
title: "Sed N"
date: 2024-11-19T14:19:25+03:00
draft: false
description: 
noindex: false
featured: false
pinned: false
# comments: false
series:
  - regex
categories:
  - blog
tags:
  - sed
  - find
  - posix
images:
  - reg1.png
weight: 98
authors:
  - ra

# menu:
#   main:
#     weight: 100
#     params:
#       icon:
#         vendor: bs
#         name: book
#         color: '#e24d0e'
---

Примеры использования поисковых запросов POSIX

<!--more-->
{{< bs/alert info >}}
Потоковый редактор SED. Обзор опции -n
{{< /bs/alert >}}


## -n \-\-quiet \-\-silent

Это полезная опция, которая выводит только строки, которые удовлетворяют запросам в выражении, по умолчанию выводится весь текст и дублируются строки, удовлетворяющие запросу.

У этой опции три варианта написания:
 - `-n` 
 - `--quiet` 
 - `--silent`
 
 все равноправные.
 
Пример: 
```sh
╭─edge@edge-manjaro in ~/tmp/sed 
╰$ seq 3 | sed -E -e  '2ia' -e '2ai' -e '3c100'  
1
a
2
i
100
```
а теперь поставим `-n`:
```shell
╭─edge@edge-manjaro in ~/tmp/sed 
╰$ seq 3 | sed -E -n -e '2ia' -e '2ai' -e '3c100' 
a
i
100
```
вывелись только те строки, в которых были изменения

В этом примере использую опцию `-E` потому-что нравится больше расширенная нотация и выражения читаются легче.

## Команды (i a c)

Эти ключики очень похожи друг на друга и делают вполне разумные и понятные вещи: 

### Команда (i)

{{< bs/alert secondary >}}
Добавляет текст перед строкой
{{< /bs/alert >}}

Синтаксис: 

`i text`

`i\ text`

Второй вариант удобен в скриптовых файлах, где шаблон можно писать в несколько строк

```shell
i\
text
```
### Команда (a)

{{< bs/alert secondary >}}
Добавляет текст после строки
{{< /bs/alert >}}

Синтаксис: 

`a text`

`a\ text`

Пример: добавим слово `text` после 5-й строки.

```shell
╭─edge@edge-manjaro in ~/tmp/sed 
╰$ seq 6 | sed -E '5a text'
1
2
3
4
5
text
6

```

### Команда (c)

{{< bs/alert secondary >}}
Заменяет текст в строке
{{< /bs/alert >}}

Синтаксис: 

`с text`

`с\ text`

Пример: заменим 3-ю строку на слово `text5`

```shell
╭─edge@edge-manjaro in ~/tmp/sed 
╰$ seq 4 | sed -E '3c text5' 
1
2
text5
4
```

Обзор документации по SED в разделе **Справочник**. [Подробнее..]({{% relref "/docs/linux/sed" %}})
