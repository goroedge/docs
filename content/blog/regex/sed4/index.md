---
title: "Sed [Разделители и команды f i I ]"
date: 2024-11-21T14:18:44+03:00
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
  - sed4.png
weight: 101
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
Потоковый редактор SED. Разделители в запросах и обзор команд [f i I ]
{{< /bs/alert >}}

## Примеры с редактором SED

### Разделители в командах регулярных выражений 

Ещё один прикол. 
Разделителем в запросе регулярного выражения может быть любой символ. 
ставим `\` дальше разделитель, потом шаблон и опять разделитель. 
т.е. `/abc/d` --- удалит все строки где есть abc, но 
`\-abc-d` или `\%abc%d` или `\eabced` --- все сделают тоже самое 

```shell
╭─edge@edge-manjaro in ~/data/sites/hb3 on main ✘ (origin/main +7 -1)
╰$ printf "aaa\nbbb\nccc\nddd\n" | sed -E '\%ddd%sadaYap'
aaa
bbb
ccc
Ydd
Ydd
```
в этом примере разделителем были `%` вокруг маски `ddd`, и `a` вокруг шаблонов замены буквы `d` на `Y`. 

Команда замены `s///` и команда вывода в выходной поток `p`.

### Файлы с командами ключ -f

#### Создадим файл с командой для SED

```shell
cat > g.sed
/abc/s/b/X/p
^Z
```
и выполним команду 

``` shell

echo abcdef | sed -n -f g.sed
aXcdef

```
{{< bs/alert danger >}}
Сработало!
{{< /bs/alert >}}

во второй строке примера буква `b` заменилась на `X`, как мы и прописали в примере.

ключ `-f g.sed` и имя файла с шаблонами и командами

Сложные команды в файлах писать гораздо удобнее и каждая новая команда с новой строки.

#### Пример по сложнее
Создадим файл h.sed

``` shell
{/[abc]/i\
:start->
=
s/[abc]/Y/p
a\
:end
}
```
{{< bs/alert info >}}
По нашему замыслу: при нахождении в строке любой из букв a, b или c, выполняем вставку перед строкой записки :start->. Затем вставляем номер строки =. И заменяем найденную букву на Y. В завершение печатаем после строки :end.

{{< /bs/alert >}}

и выполним команду:

``` shell
╭─edge@edge-manjaro in ~/tmp/sed 
╰$ printf "aaa\nbbb\nccc\nddd\n" | sed -E -f h.sed       
:start->
1
Yaa
Yaa
:end
:start->
2
Ybb
Ybb
:end
:start->
3
Ycc
Ycc
:end
4
ddd
:end

```
Все сработало! В трех строках были найдены шаблоны и выполнена замена. В четвертой замена не выполнена, потому-что нет букв `[abc]`.

### Команда i и I 

{{< bs/alert info >}}
Назначение опций: сохранять backup изменяемого файла в другом файле с добавлением расширения.

{{< /bs/alert >}}

Очень долго бился, пока до меня дошло, что `-i .bac` добавляет к старому файлу расширение .bac, и сохраняет предыдущие значения, а изменения будут в
первоначальном файле.

Так вот `i` от `I` отличается нумерацией строк в потоке: 

`-I` нумерует все подряд, т.е. в 10-м файле нумерация продолжится после девятого. 

`-i` в каждом файле нумерацию начинает с 1. Все, больше никакой
разницы.

Создадим файл `a.txt`:

``` shell
╭─edge@edge-manjaro in ~/tmp/sed 
╰$ cat > a.txt
aaa aaaa aaaaa
^Z
[1]  + 10182 suspended  cat > a.txt

```
Создадим файл b.txt и c.txt

``` shell
╭─edge@edge-manjaro in ~/tmp/sed 
╰$ sed -n 's/a/b/pg' < a.txt > b.txt

╭─edge@edge-manjaro in ~/tmp/sed 
╰$ cat b.txt
bbb bbbb bbbbb

╭─edge@edge-manjaro in ~/tmp/sed 
╰$ sed -n 's/a/c/pg' < a.txt > c.txt

╭─edge@edge-manjaro in ~/tmp/sed 
╰$ cat c.txt                        
ccc cccc ccccc

```

Файлы b.txt и c.txt я создал также через милый запрос SED. Которому на вход подал файл `< a.txt`, а на выход файлы `> b.txt` и `> c.txt`, соответственно.

А теперь наша задумка с ключами `i` и `I`.

``` shell
╭─edge@edge-manjaro in ~/tmp/sed 
╰$ sed -E -i\.bc '{=;/[abc]/s/[abc]/YX/p;}' a.txt b.txt c.txt 

╭─edge@edge-manjaro in ~/tmp/sed 
╰$ ls
a.txt    b.txt.bc 
a.txt.bc  c.txt 
b.txt    c.txt.bc 

╭─edge@edge-manjaro in ~/tmp/sed 
╰$ cat a.txt
1
YXaa aaaa aaaaa
YXaa aaaa aaaaa

╭─edge@edge-manjaro in ~/tmp/sed 
╰$ cat b.txt
1
YXbb bbbb bbbbb
YXbb bbbb bbbbb

╭─edge@edge-manjaro in ~/tmp/sed 
╰$ cat c.txt
1
YXcc cccc ccccc
YXcc cccc ccccc

```
В каждом файле нумерация строк начинается с `1`.

А теперь выполним тоже самое но с ключем `I` 
{{< bs/alert warning >}}

Ключ I работает только на FREEBSD на LINUX не работает.
{{< /bs/alert >}}

``` shell
╭─edge@edge-bsd in ~/tmp/sed 
╰$ sed -E -I\.bc '{=;/[abc]/s/[abc]/YX/p;}' a.txt b.txt c.txt 

╭─edge@edge-bsd in ~/tmp/sed 
╰$ ls
a.txt    b.txt.bc 
a.txt.bc  c.txt 
b.txt    c.txt.bc 

╭─edge@edge-bsd in ~/tmp/sed 
╰$ cat a.txt
1
YXaa aaaa aaaaa
YXaa aaaa aaaaa

╭─edge@edge-bsd in ~/tmp/sed 
╰$ cat b.txt
2
YXbb bbbb bbbbb
YXbb bbbb bbbbb

╭─edge@edge-bsd in ~/tmp/sed 
╰$ cat c.txt
3
YXcc cccc ccccc
YXcc cccc ccccc

```
в каждом файле нумерация строк продолжается 1,2,3.
