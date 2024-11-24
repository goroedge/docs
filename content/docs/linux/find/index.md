---
title: "Find"
# linkTitle:
date: 2024-11-18T16:04:18+03:00
draft: false
description: "Удивительная утилита, которая может найти все на диске и еще выполнить над тем, что нашла, все что угодно!"
featured: false
noindex: false
# comments: false
nav_weight: 1000
# nav_icon:
#   vendor: bootstrap
#   name: toggles
#   color: '#e24d0e'
series:
  - linux
categories:
  - docs
tags:
  - find
  - zsh
  - admin
  
images:
  - find.png

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

Удивительная утилита, которая может найти все на диске и еще выполнить над тем, что нашла, все что угодно!
<!--more-->

## Командная строка find


```sh
find [path...] [expression]
```

Аргумент `path` указывает директорию или список директорий с которой начинаем поиск.

Аргумент `expression` состоит из опций, тестов и действий. Одно выражение может объединять любое их количество, используя традиционные булевы операторы, такие как and и or.

### OPTION

- -d, -depth: указывает на проход утилиты вглубь в дочерние каталоги
- -mindepth, -maxdepth: уровень обработки каталогов вглубь

### TESTS

Тесты --- это основные команды утилиты.

- `-name`: проверяет, соответствует ли имя файла шаблону (использует простое сопоставление с шаблоном и смотрит только на имя файла)
- `-regex`: проверяет, соответствует ли имя файла шаблону (использует стандартные регулярные выражения Emacs и проверяет **полный путь** к файлу)
- `-type`: проверяет, относится ли файл к определенному типу (`f` -- обычный файл, `d` -- каталог, `s` -- символическая ссылка и т. д.)

```sh
╭─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find . -name "*.svg"
./content/docs/latex/pdfpages/adobe-pdf-icon.svg
./content/docs/latex/pdfpages/adobe-pdf-2.svg
./content/docs/linux/ssh/ssh.svg
./themes/hugo-theme-relearn/exampleSite/static/images/logo.svg
```

`.` --- это поиск в текущей директории

`-name` --- ищем файлы с именами по шаблону

```zsh
╭─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find config -type d 
config
config/_default
```
выведем только директории в каталоге `config`

### Работа со временем

 - `-amin, -anewer, -atime`: --- проверяет последние изменения в файлах
 - `-cmin, -cnewer, -ctime`: --- проверяет время создания файлов относительно времени другого файла
 - `-mmin, -mnewer, -mtime`: --- проверяет время последнего изменения файла
 - `-newer`: --- сравнивает файлы новее исходного
 
 ```sh
 ╭─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find . -name "*.png" -ctime -2
./public/docs/emacs/yasnippet/logo.png
./public/docs/emacs/magit/magit.png
./public/docs/latex/newfont/121751.png
./public/docs/latex/pdfpages/adobe.png
./public/docs/latex/titleps/131227.png
./public/docs/latex/titlesec/101100.png
./public/docs/latex/titlesec/101034.png
./public/docs/latex/titlesec/101112.png
```
вывести все файлы с расширением `.png`, созданные в течение последних двух дней

```sh
─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find . -newer ./public/docs/linux/ssh/ssh.png

./public
./public/tags/index.html
./public/tags/index.xml
./public/tags/documentation/index.html
./public/tags/documentation/index.xml
./public/tags/soft/index.html

```
вывести все файлы, которые новее `ssh.png`

### Поиск по свойствам файлов

 - `-perm`: поиск по правам доступа файла
 - `-size`: поиск по размеру файла
 
 ```sh
 ╭─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find . -perm 777
./assets/images/big.jpg
./assets/images/width-title.jpg
./assets/images/logo.png
```

поиск всех файлов с правами `777`

```sh
╭─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find . -size 2M
./assets/images/ig.png
./themes/hugo-theme-relearn/exampleSite/content/introduction/quickstart/magic.gif
./themes/hugo-theme-relearn/static/js/mathjax/mml-svg.js
```
поиск файлов размером больше 2М

### Действия над найденными файлами

 - `-ls`: выводит результат в формате `ls`
 - `-print, -print0, -printf`: вывод результата в стандартный поток вывода
 - `-fprint, -fprint0, -fprintf`: вывод результата в файл
 
```sh
╭─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find . -name "ssh*" -ls
   502782      0 drwxr-xr-x   1 edge     edge           62 ноя 15 17:44 ./content/docs/linux/ssh
   502783      8 -rw-r--r--   1 edge     edge         7865 ноя 13 11:52 ./content/docs/linux/ssh/ssh.svg
   502784    136 -rw-r--r--   1 edge     edge       136846 ноя 13 11:53 ./content/docs/linux/ssh/ssh.png
   502907      0 drwxr-xr-x   1 edge     edge           70 ноя 14 17:55 ./public/ru/docs/linux/ssh
   502853      0 drwxr-xr-x   1 edge     edge          114 ноя 14 19:42 ./public/docs/linux/ssh
   502854    136 -rw-r--r--   1 edge     edge       136846 ноя 17 19:26 ./public/docs/linux/ssh/ssh.png
   502855      8 -rw-r--r--   1 edge     edge         7865 ноя 17 19:26 ./public/docs/linux/ssh/ssh.svg
```
выводит все файлы, где в имени есть `ssh`

```sh
╭─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find . -name "ssh*" -printf '%s %p\n'
62 ./content/docs/linux/ssh
7865 ./content/docs/linux/ssh/ssh.svg
136846 ./content/docs/linux/ssh/ssh.png
70 ./public/ru/docs/linux/ssh
114 ./public/docs/linux/ssh
136846 ./public/docs/linux/ssh/ssh.png
7865 ./public/docs/linux/ssh/ssh.svg
```
выводит только размер и имя

 - `-delete`: удаляет все найденные файлы
 - `-exec`: выполняет любую команду над результатом поиска
 
 ```sh
 find /tmp -name "*.tmp" -delete
 ```
 удалит все файлы с расширением `tmp`
 
 ```sh
 ─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find . -name "*.yaml" -type f -exec grep -l doc {} \;  
./themes/hugo-theme-relearn/.github/actions/release_milestone/action.yaml
./themes/hugo-theme-relearn/.github/workflows/docs-build-deployment.yaml
./themes/hugo-theme-relearn/.github/workflows/docs-build.yaml
```

найдет все файлы с расширением `yaml` в которых есть слово `doc`

{{< bs/alert warning >}}
В конце команды `-exec` обязательно поставить `{}` --- результат выборки и в самом конце `\;` чтобы команда выполнилась над файлом 1 раз, если использовать `+` то в `grep` , будут переданы несколько файлов.

{{< /bs/alert >}}

```sh
╭─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find . -name "*.yaml" -type f | xargs grep -l doc      
./themes/hugo-theme-relearn/.github/actions/release_milestone/action.yaml
./themes/hugo-theme-relearn/.github/workflows/docs-build-deployment.yaml
./themes/hugo-theme-relearn/.github/workflows/docs-build.yaml

```
это альтернативная команда `xargs` вместо `exec`. Получает на вход результат `find` и выполняет свою команду.

{{< bs/alert danger >}}
XARGS работает в разы быстрее EXEC
{{< /bs/alert >}}


### Операторы Find

Операторы можно комбинировать как обычные логические выражения

(expr): это обычные круглые скобки
!, -not: оператор отрицания `НЕТ`
-a, -and: оператор логическое `И`
-o, -or: оператор логическое `ИЛИ`

### Расширенные параметры

```sh
find [-H] [-L] [-P] [-Olevel] [-D help|tree|search|stat|rates|opt|exec] [path] [expressions]
```
 - `H, L, P` --- порядок обработки символических ссылок
 - `O` --- уровень оптимизации от 0 до 3
 - `D` --- диагностическая информация
 
 
## REGEX

{{< bs/alert info >}}
Команда FIND в сочетании с регулярными выражениями и другими командами оболочки, становится супер инструментом.
{{< /bs/alert >}}

```sh
find [path] [expression]
```

Этот раздел посвящен простому слову в команде `exptession`

```sh
find [path] -regex [regular_expression]

```
Будет выполнен поиск по указанному пути и возвращен список файлов, удовлетворяющих условию.

{{< bs/alert warning >}}
Шаблон regular_expression включает полное имя файла, включая корневой путь к каталогу.
{{< /bs/alert >}}

```sh

╭─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find ./ -type f -regex '.*css\/*'
./themes/hugo-theme-relearn/assets/css/auto.css
./themes/hugo-theme-relearn/assets/css/chroma-learn.css
./themes/hugo-theme-relearn/assets/css/chroma-neon.css
./themes/hugo-theme-relearn/assets/css/chroma-relearn-dark.css
./themes/hugo-theme-relearn/assets/css/chroma-relearn-light.css
./themes/hugo-theme-relearn/assets/css/format-print.css

```
выдал все файлы в которых есть в наименовании `css/`

```sh
╭─edge@edge-manjaro in ~/data/sites/doc10 on master ✘ 
╰$ find ./ -type f -regex '.*neon.*'
./themes/hugo-theme-relearn/assets/css/chroma-neon.css
./themes/hugo-theme-relearn/assets/css/theme-neon.css
./public/css/theme-neon.css
./public/css/chroma-neon.css

```
а в этом запросе должен быть `neon`

{{< bs/alert secondary >}}
Для поиска через FIND всегда результат будет начинаться с ./, а это значит что в регулярном выражении мы должны поставить \.\/ - т.е экранировать точку и косую черту 
{{< /bs/alert >}}

### Команда -iregex

```sh
find [path] -iregex [regular_expression]
```
почти тоже самое, только с регистронезависимым поиском. Будет искать и большие и маленькие буквы.

### Команда -regextype

Выбирает тип регулярного выражения
 - findutils
 - emacs --- установлено по умолчанию
 - gnu-awk
 - grep
 - egrep
 - posix-awk
 - posix-basic
 - posix-egrep
 - posix-extended

На этой странице есть описание всех синтаксисов регулярных выражений {{< bs/alert-link "https://www.gnu.org/software/findutils/manual/html_node/find_html/Regular-Expressions.html" "https://www.gnu.org/software/findutils/manual/html_node/find_html/Regular-Expressions.html" >}}
