---
title: "ZSH"
# linkTitle:
date: 2024-11-17T21:29:09+03:00
draft: false
description: 
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
  - zsh
  - shell
  - oh-my-zsh
images:
  - logo.png
# menu:
#   main:
#     weight: 100
#     params:
#       icon:
#         vendor: bs
#         name: book
#         color: '#e24d0e'
---

Командная оболочка ZSH и все о ней

<!--more-->
{{< bs/alert info >}}
Первая версия ZSH была написана Паулем Фалстадом, когда он был студентом Принстонского университета в 1990 году. Название оболочки произошло от учетной записи "zsh" университетского ассистента Пауля по имени Чжун Шао. В настоящее время проект развивается энтузиастами под руководством Питера Стефенсона в рамках свободно распространяемого ПО.

{{< /bs/alert >}}

ZSH является расширенным аналогом BASH и имеет с ним обратную совместимость, добавляя ему большое количество улучшений.


## Установка по умолчанию ZSH

{{< bs/alert primary >}} Официальный сайт {{< bs/alert-link "https://www.zsh.org/" "https://www.zsh.org/" >}}
 американское зеркало {{< bs/alert-link "https://zsh.sourceforge.io/" "https://zsh.sourceforge.io/" >}}
 документация на `zsh` {{< bs/alert-link "https://zsh.sourceforge.io/Doc/Release/zsh_toc.html" "https://zsh.sourceforge.io/Doc/Release/zsh_toc.html" >}}

{{< /bs/alert >}}

Проверить текущую оболочку 
```sh
$ echo $SHELL
```

Проверить какие оболочки установлены
```sh
chsh -l
```

Установить по умолчанию zsh:
```sh
chsh -s /bin/zsh/
```

Если не установлен, то в Manjaro выполнить
```sh
sudo pacman -S zsh
zsh
```

если скрипт не запустился, то

```sh
autoload -Uz zsh-newuser-install
zsh-newuser-install -f
```

## Поставим OH-MY-ZSH

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Читаем документацию https://github.com/ohmyzsh/ohmyzsh/wiki

## Редактируем `~/.zshrc`

`1. export ZSH="$HOME/.oh-my-zsh"` --- путь к настройкам `oh-my-zsh`

`2. ZSH_THEME="strug"` --- тема оформления shell-а.
![Образец](172151.png ) 

{{< highlight sh "hl_lines=3,linenostart=3" >}}
// 

plugins=(git
    bundler
    copyfile
	copybuffer
    copypath
    cp
    emacs
    node
    npm
    qrcode
    rsync
)

{{< / highlight >}}

Продолжение настройки: подключаем плагины

`19. source $ZSH/oh-my-zsh.sh` --- определяю источник для доступа к репозиторию `oh-my-zsh`

`20. EDITOR='emacs'` --- назначаю редактор по умолчанию `Emacs`

`21. [[ -s /home/edge/.autojump/etc/profile.d/autojump.sh ]] && source /home/edge/.autojump/etc/profile.d/autojump.sh
` --- подключаю модуль `autojump` т.к. он отказался подключаться по умолчанию и его пришлось устанавливать в ручную.

{{< bs/alert warning >}}
О каждом модуле подробнее
{{< /bs/alert >}}

### autojump

{{< bs/alert info >}}

Прыгает по директориям. Очень удобно.
{{< /bs/alert >}}

Установка из репозитория https://github.com/wting/autojump

настройка обязательно написать в строке ~/.zshrc
```sh
[[ -s /home/edge/.autojump/etc/profile.d/autojump.sh ]] && source /home/edge/.autojump/etc/profile.d/autojump.sh
```
1. `j foo` --- быстро переходит в директорию, в которой уже переходили по `cd `
2. `jc bar` --- переходит в дочернюю диреторию не набирая `cd`
3. `jo music` --- откроет директорию в стандартном файловом менеджере
4. `jco images` --- откроет дочернюю диреторию в стандартном файловом менеджере

### bundler

### copyfile 

{{< bs/alert info >}}

Копирует содержимое файла в буфер обмена, чтобы потом вставить в другое место.

{{< /bs/alert >}}

```sh
copyfile <filename>
```
### copybuffer

{{< bs/alert info >}}

Копирует тукущую команду в строке в буфер обмена, чтобы потом вставить в другое место.

{{< /bs/alert >}}

```sh
copybuffer
```
или горячая клавиша `C-o`

### copypath 

{{< bs/alert info >}}

Копирует текущую дирректорию в буфер обмена, чтобы потом вставить в другое место.

{{< /bs/alert >}}

```sh
copypath
```

### cpv (модуль cp)
{{< bs/alert info >}}

Копирует файлы или директории с сохранением Backup, прав доступа и показывает прогресс. Использует функцию `rcync`

{{< /bs/alert >}}

```zsh
cpv() {
    rsync -pogbr -hhh --backup-dir="/tmp/rsync-${USERNAME}" -e /dev/null --progress "$@"
}
compdef _files cpv
```
Получает что-то вроде:
```sh
cpv doc10 doc11

doc10/themes/hugo-theme-relearn/static/
doc10/themes/hugo-theme-relearn/static/css/
doc10/themes/hugo-theme-relearn/static/css/auto-complete.css
          1,75K 100%    1,75kB/s    0:00:00 (xfr#2254, to-chk=199/3084)
doc10/themes/hugo-theme-relearn/static/css/fontawesome-all.min.css
         94,26K 100%   94,54kB/s    0:00:00 (xfr#2255, to-chk=198/3084)
doc10/themes/hugo-theme-relearn/static/css/fonts.css
          2,72K 100%    2,73kB/s    0:00:00 (xfr#2256, to-chk=197/3084)
```
### emacs

{{< bs/alert info >}}

Создает несколько мощных ALIASES для работы с `emacs`

{{< /bs/alert >}}

1. `emacs`	--- открывает редактор с файлом
2. `e` --- аналогично `emacs`	
3. `te`	--- открывает клиента emacs в терминале
4. `eeval`	--- выполняет команду `M-x eval` не открывая Emacs
5. `eframe`	--- откроет новый frame emacs
6. `efile`	---	печатает текущий путь файла в буфер
7. `ecd`	---	печатает тукущую директорию в буфер

Теперь, чтобы открыть этот файл мне нужно набрать:
```sh
j hb3
e content/docs/linux/zsh/index/md
```

и я продолжаю работать. Но это еще не все.

### ecode64
{{< bs/alert info >}}

Создает текст и файлы в формате `base64`

{{< /bs/alert >}}

Нужно для отправки картинок по почте, вставки на сайты в код и т.д. Иногда пользуюсь, поэтому поставил.
Функция | Алиас | Описание
--------|-------|----------
encode64|	e64|	Кодирует в base64
encodefile64|	ef64	|Кодирует файл в base64 и помещает в одноименный файл с расширением `.txt`
decode64|	d64|Декодирует из base64

```sh
╭─edge@edge-manjaro in ~ 
╰$ e64 "Игорь Ра"
0JjQs9C+0YDRjCDQoNCw
╭─edge@edge-manjaro in ~ 
╰$ 


╭─edge@edge-manjaro in ~ 
╰$ d64 0JjQs9C+0YDRjCDQoNCw
Игорь Ра%
╭─edge@edge-manjaro in ~ 
╰$ 


╭─edge@edge-manjaro in ~ 
╰$ echo "Игорь Ра" | e64
0JjQs9C+0YDRjCDQoNCwCg==


╭─edge@edge-manjaro in ~ 
╰$ echo "0JjQs9C+0YDRjCDQoNCwCg==" | d64
Игорь Ра

```

```sh
// Создам файл
╭─edge@edge-manjaro in ~ 
╰$ > etest.txt    
Пример файла
^Z
[1]  + 8113 suspended   > etest.txt

// Закодирую файл
╭─edge@edge-manjaro in ~ 
╰$ ef64 etest.txt 
etest.txt's content encoded in base64 and saved as etest.txt.txt

// Посмотрим, что получилось
╭─edge@edge-manjaro in ~ 
╰$ cat etest.txt.txt 
0J/RgNC40LzQtdGAINGE0LDQudC70LAK
```

### git

{{< bs/alert info >}}

Это целая фабрика ALIASES для git

{{< /bs/alert >}}

Легче посмотреть документацию, чем перечислять здесь: {{< bs/alert-link "https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git" "https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git" >}}

Самые ключевые команды:
Алиас | Команда
------|--------
g|git
ga	|git add
gaa	|git add --all
gam	|git am
gb	|git branch
gco	|git checkout
gccd|	git clone --recurse-submodules "$@" && cd "$(basename $\_ .git)"
gcam|	git commit --all --message
gcmsg|	git commit --message
gd|	git diff
gf|	git fetch
gfo|	git fetch origin
gl|	git pull
gp|	git push
gpf!|	git push --force
gpod|	git push origin --delete
grb	|git rebase
gr|	git remote
grset|	git remote set-url
grm	|git rm
gsh	|git show
gst	|git status

### pass

{{< bs/alert info >}}

Работает из терминала с программой PASS

{{< /bs/alert >}}

Требует отдельной статьи, т.к. очень серьезная программа для хранения паролей.

### qrcode
{{< bs/alert info >}}

Генерит QRcode в TXT и SVG

{{< /bs/alert >}}

Передаем текст в сервис {{< bs/alert-link "https://qrcode.show/" "https://qrcode.show/" >}}

Алиас | Комманда
-----|--------
qrcode [text]|	curl -d "text" qrcode.show
qrsvg  [text]|	curl -d "text" qrcode.show -H "Accept: image/svg+xml"

```sh
qrsvg "Игорь Ра"
<?xml version="1.0" standalone="yes"?><svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="330" height="330" viewBox="0 0 330 330" shape-rendering="crispEdges"><rect x="0" y="0" width="330" height="330" fill="#fff"/><path fill="#000" d="M40 40h10v10H40V40M50 40h10v10H50V40M60 40h10v10H60V40M70 40h10v10H70V40M80 40h10v10H80V40M90 40h10v10H90V40M100 40h10v10H100V40M120 40h10v10H120V40M160 40h10v10H160V40M190 40h10v10H190V40M200 40h10v10H200V40M2
```

```sh
╭─edge@edge-manjaro in ~/data/sites 
╰$ qrcode "Игорь Ра"
█████████████████████████████████
█████████████████████████████████
████ ▄▄▄▄▄ █ ▀▀▀▄██▄ █ ▄▄▄▄▄ ████
████ █   █ █▄█ ▄▀██▄ █ █   █ ████
████ █▄▄▄█ █▄▀▄▀██▄  █ █▄▄▄█ ████
████▄▄▄▄▄▄▄█▄█▄█▄▀▄▀ █▄▄▄▄▄▄▄████
████▄█▀ ▄ ▄ ▄▀█ ▀ ██ ▄▀█▄█   ████
████▄  ▀▀▄▄▀█▄  █ █▄▀▀▀▄▄▄█▀▀████
████  ▄█▀█▄█▄  ▄▄ ▀ █▄▄█▄██ ▀████
████ ▄ ▀█▄▄▀██▀ ▄▄██ █ ▄▀▀██▀████
████▄██▄▄▄▄▄▀▀▄▀▀▀   ▄▄▄ █▀▄ ████
████ ▄▄▄▄▄ █ ▀ ▄▀█▀  █▄█ ▄ ▀█████
████ █   █ █ ███▄▄ █  ▄▄ ▀█▄▀████
████ █▄▄▄█ ██ ▀█▄█ ▄█▀ ▀█ ▄  ████
████▄▄▄▄▄▄▄█▄▄███▄▄▄█▄▄▄▄█▄█▄████
█████████████████████████████████
▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀
```

### rcync

{{< bs/alert info >}}

Любимая команда для копирования, перемещения и синхронизации

{{< /bs/alert >}}

Можно этой команде посвящать отдельный пост. Но в этом случае имеем четыре Алиаса:

Алиас | Команда| Описание
------|--------|------
rsync-copy|	rsync -avz --progress -h| Копирует файлы и директории
rsync-move|	rsync -avz --progress -h --remove-source-files| перемещает файлы и директории
rsync-update|	rsync -avzu --progress -h| обновляет файлы
rsync-synchronize|	rsync -avzu --delete --progress -h| синхронизирует 

{{< bs/alert warning >}}
Для этого сайта использую команду
{{< /bs/alert >}}

```sh
hugo && rsync-synchronize ~/data/sites/hb3/public/ ftp_name@server.name:~/public_html/
```
