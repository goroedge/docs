---
title: "Sed команды [q r w ]"
date: 2024-11-22T14:18:44+03:00
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
  - sed5.png
weight: 102
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
	Потоковый редактор SED. Обзор команд [q r w ]
{{< /bs/alert >}}

## Примеры с редактором SED


### Команда q

просто прерывает выполнение поиска в регулярном выражении

в Linux еще есть вариант с возвращением кода выхода `q[exit-code]` и `Q[exit-code]`, последняя не печатает контент в выходной поток, но Freebsd этот формат не поддерживает.

### Команда r filename и в Linux R filename

вставляет в выходной поток целый файл

у меня есть заголовленный файлик с непонятным текстом: `a.txt` я над ним ставил примеры в прошлом уроке, но это не имеет значения. Сейчас смотрим, как команда `r` добавит этот файлик в выходной поток.
```shell
╭─edge@bsd in ~/tmp 
╰$ printf "aaa\nbbb\nc\tcc\nuuu\n" | sed -El '/[abc]/{s/[adb\t]/f/p;G;};ra.txt' 
faa
faa

// от этого момента начинается добавление файла a.txt
1
dDddddDddddDddd dDddddDddddDddddDddddDddd aaaaa
2
dDddddDddddDddd dDddddDddddDddddDddddDddd aaaaa
3
dDddddDddddDddd dDddddDddddDddddDddddDddd aaaaa
4
dDddddDddddDddd dDddddDddddDddddDddddDddd aaaaa
// здесь заканчивается фалик a.txt
fbb
fbb
```

итог: файлик вставился после первой обработанной строки и началась обработка второй строки.

### Я эту команду назвал `N`

потому-что эта команда выполняет обработку шаблона не в первом совпадении а в совпадении N. В моем примере я указал `2p`. То-есть второе совпадение изменить и вывести информацию в выходной поток командой `p`. Для глобальной замены в строке всех совпадений, используем флаг: `g`, т.е. мне нужно было написать `gp`.

```shell
╭─edge@bsd in ~/tmp 
╰$ printf "aaa\nbbb\nc\tcc\nuuu\n" | sed -El '/[abc]/{s/[adb\t]/f/2p;}'      
afa
afa
bfb
bfb
c       cc
uuu
```
### Команда `w`

Команда `w filename` может быть и как отдельная команда и как флаг после команды `s`

```shell
╭─edge@bsd in ~/tmp 
╰$ printf "aaa\nbbb\nc\tcc\nuuu\n" | sed -El '/[abc]/s/[adb\t]/f/pw 2.out'
faa
faa
fbb
fbb
cfcc
cfcc
uuu
```

собственно ее действие, все что было изменено отправить в выходной файл `w file`, а что не было изменено,то не отправлять.

Данная команда отличается от перенаправления выходного потока `> file`.
