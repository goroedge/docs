+++
title = 'Строчный редактор SED'
linktitle = 'Edit SED'
date = 2024-11-15T11:19:52+03:00
categories = 'docs'
series = 'linux'
tags = 'documentation'
summary = 'Описание команд потокового редактора SED'
description = 'Основные команды редактора SED'
images = ['sed.png']
authors = 'ra'
+++

## Кто такой SED?

{{< bs/alert info >}}


Sed - это неинтерактивный строчный редактор. Он принимает текст либо с устройства stdin, либо из текстового файла, выполняет некоторые операции над строками и затем выводит результат на устройство stdout или в файл. Как правило, в сценариях, sed используется в конвейерной обработке данных, совместно с другими командами и утилитами.
{{< /bs/alert >}}
## Синтаксис SED



```shell
Использование: sed [ПАРАМЕТР]… {только-сценарий-если-нет-другого-сценария}
               [входной-файл]…

  -n, --quiet, --silent
                 выключить автоматическую печать образца
      --debug
                 комментировать выполнение программы
  -e script, --expression=сценарий
                 добавить сценарий в исполняемые команды
  -f script-file, --file=файл-сценария
                 добавить содержимое файла-сценария в исполняемые команды
  --follow-symlinks
                 переходить по символьным ссылкам при обработке на месте
  -i[СУФФИКС], --in-place[=СУФФИКС]
                 править файлы на месте (создаёт копию, если указан СУФФИКС)
  -l N, --line-length=N
                 задать желаемую длину до переноса строки для команды «l»
  --posix
                 отключить все расширения GNU
  -E, -r, --regexp-extended
                 использовать в сценарии расширенные регулярные выражения
                 (для переносимости используйте -E (POSIX)
  -s, --separate
                 рассматривать файлы раздельно, а не в виде одного
                 длинного непрерывного потока
      --sandbox
                 работать в режиме «песочницы»
                 (отключает команды e/r/w)
  -u, --unbuffered
                 загружать минимальный объём данных из входных файлов
                 и чаще сбрасывать выходные буферы на диск
  -z, --null-data
                 разделять строки символами NUL
      --help     показать эту справку и выйти
      --version  показать информацию о версии и выйти

Если не указан параметр -e, --expression, -f или --file, то в качестве
интерпретируемого сценария sed берётся первый необязательный аргумент.
Все оставшиеся аргументы являются именами входных файлов; если входные
файлы не указаны, тогда читается стандартный ввод.

Домашняя страница GNU sed: <https://www.gnu.org/software/sed/>.
Справка по работе с программами GNU: <https://www.gnu.org/gethelp/>.
Сообщения об ошибках отправляйте на <bug-sed@gnu.org>.
```

## Обзор опций SED

Опции настолько интересны, что я решил сделать в блоге специальный раздел для примеров по каждой опции по тегу `#regexp`

`--version` --- очевидно выведет версию `SED`

`--help` --- смотрим предыдущий раздел

### -n \-\-quiet \-\-silent

Это полезная опция, которая выводит только строки, которые удовлетворяют запросам в выражении, по умолчанию выводится весь текст и дублируются строки, удовлетворяющие запросу.

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

## Работа с SED
Для образца, я загнал в файл sed.txt help
```shell
sed --help > sed.txt
```
Дальше работаю с этим файлом

### ключ `p`: 
--- выводит строки в терминал (важно использовать параметр `- n`, а то выведет весь файл и продублирует условие отбора.

```shell
sed -n /script/p sed.txt

-e script, --expression=сценарий
-f script-file, --file=файл-сценария
```
вывести 5-ю строку `sed -n 5p sed.txt`

вывести с 1-й по 5-ю строку `sed -n 1,5p sed.txt`

вывести c 35-й строки до конца файла `sed -n '35,$p' sed.txt`

вообще лучше приучить себя ставить команды в апострофы, либо \' , либо \"

### ключ `d`:

--- удаляет строку с выполненным условием

	8d --- удалить 8-ю строку
	/^$/d --- Удалить все пустые строки.
	1,/^$/d	--- Удалить все строки до первой пустой строки, включительно.
	/GUI/d	--- Удалить все строки, содержащие "GUI".

### ключ `s`:

--- заменяет по условию

	's/Windows/Linux/'	В каждой строке, заменить первое встретившееся слово "Windows" на слово "Linux".
	's/BSOD/stability/g' В каждой строке, заменить все встретившиеся слова "BSOD" на "stability".
	's/ *$//'	        Удалить все пробелы в конце каждой строки.
	's/00*/0/g'	        Заменить все последовательности ведущих нулей одним символом "0".
	'1,3 s/unix/linux/' Заменить в 1-й по 3-ю строки

### ключ `g`:
--- выполняет глобальную замену всех вхождений
	's/unix/linux/g'    Заменить все вхождения в строке
	's/unix/linux/1'    Заменить только первое вхождение в строке
	's/unix/linux/3'    Заменить только третье вхождение в строке
	's/unix/linux/3g'    Заменить все вхождения начиная с 3-го в строке
### ключ `i`
игнорирует регистр в шаблоне

Синтаксис: `sed 's/old_pattern/new_pattern/i' filename`
Пример: `sed 's/life/Love/i' a.txt`
### скрипт

1. `/что искать/` --- просто пишем регулярное выражение, что будем искать.

2. `G` --- пустая строка. 

Добавить пустые строки во всем файле:

	sed G sed.txt

3. вставить 2 пустые строки `G;G`

знак `;` перечисляет команды в скрипте

	sed '/^$/d;G' sed.txt
	
4. удалит все пустые строки и вставит пустые после каждой строки

выполним команду:

	sed '/script/{x;p;x;}' sed.txt
	
5. вставит пустые строки над каждой где есть слово script

выполним команду:

	sed '/script/G' sed.txt
	
6. Выполнить нумерацию строк

`=` выполняет нумерацию

	sed = sed.txt | sed 'N;s/\n/\t/'
	
7. Вывести все строки, содержащие шаблон, включая следующие за каждой из них x строк:

Синтаксис: `sed -n '/pattern/,+xp' filename`
Пример: `sed -n '/learn/,+2p' a.txt`

8. Замена шаблона другим шаблоном, за исключением строки n:

Синтаксис: `sed 'n!s/old_pattern/new_pattern/' filename`
Пример: `sed -i '5!s/life/love/' a.txt`

`- n` --- отключает печать образца
если не поставить, то выведет весь файл, а если поставить, то только результат выполненной работы

для 
`- e` --- параметр редактировать файл
