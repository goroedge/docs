---
title: "Yasnippet"
date: 2024-11-13T18:14:12+03:00
draft: false
description: "Документация и настройки Yasnippet"
noindex: false
featured: false
pinned: false
# comments: false
series:
  - emacs
categories:
  - docs
tags:
  - yasnippet
images:
  - logo.png
weight: 199
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

# Yasnippet

## Установка Yasnippet

Загрузил через `M-x list-packages [RET] yasnippet`

Поместил в init.el
``` emacs-lisp
(setq yas-snippet-dirs
      '("~/.emacs.d/snippets"                 ;; personal snippets
        "/path/to/some/collection/"           ;; foo-mode and bar-mode snippet collection
        "/path/to/yasnippet/yasmate/snippets" ;; the yasmate collection
        ))

(yas-global-mode 1) ;; or M-x yas-reload-all if you've started YASnippet already.
```

Команда `M-x yas-reload-all` перегружает все сниппеты и появляется меню в Emacs

Загрузил стандартную коллекцию сниппетов

`M-x list-packages [RET] yasnippet-snippets`

## Использование снипетов

Все очень просто.
1. Набираем ключ сниппета и нажимаем `<TAB>` и сниппет загружается
2. Снипету можно назначить свою клавишу вызова на функцию `yas-expand`

```emacs-lisp
;; Bind `SPC' to `yas-expand' when snippet expansion available (it
;; will still call `self-insert-command' otherwise).
(define-key yas-minor-mode-map (kbd "SPC") yas-maybe-expand)
;; Bind `C-c y' to `yas-expand' ONLY.
(define-key yas-minor-mode-map (kbd "C-c y") #'yas-expand)

```

## Автоматическое развертывание сниппетов

```emacs-lisp
;; Function that tries to autoexpand YaSnippets
;; The double quoting is NOT a typo!
(defun my/yas-try-expanding-auto-snippets ()
  (when (bound-and-true-p 'yas-minor-mode)
      (let ((yas-buffer-local-condition ''(require-snippet-condition . auto)))
        (yas-expand))))

;; Try after every insertion
(add-hook 'post-self-insert-hook #'my/yas-try-expanding-auto-snippets)

```

Добавим в описание сниппета переменную `# condition: (and (texmathp) 'auto)`
чтобы он стал авторасширяющимся.

## Создание своих сниппетов

На примере сниппетов для `markdown`

в коллекции хранится как `markdown-mode`, это нужно знать, чтобы потом объяснить куда складывать yasnippet-у

1. Выделяю текст для сниппета 

``` markdown
{{ bs/alert warning }}

{{ /bs/alert }}
```

2. и нажимаю `C-c & C-n`, это серьезно так сложно и не забыть `&`.

Откроется окно:
``` org
# -*- mode: snippet -*-
# name: alert warning
# condition: (and (texmathp) 'auto)
# key: alert
# --
{{ bs/alert warning }}
$0
{{ /bs/alert }}

```

3. пишу значение `name`, `condition` и `key`. Где должен оказаться курсор ставлю `$0`

4. Нажимаю `C-c C-c` для сохранения сниппета. При сохранении на запрос: 
   - `Choose or enter a table (yas guesses markdown-mode):` указать markdown-mode [RET]
   - `[yas] Loaded for markdown-mode. Also save snippet buffer? (y or n)` указать `y`
   - `File to save snippet in: ~/.emacs.d/snippets/markdown-mode/alert.5` имя файла нужно обязательно исправить, чтобы при использовании сниппета была возможность выбора значений. У меня это уже 5-й alert с разными значениями, поэтому имя дал `alert.5` если сниппет будет один, то имя может быть как ключ.
   
### Фишки сниппетов

#### Обход полей при вводе снипета задаются переменными
{{< bs/alert info >}}
`$1, $2, ...` и заканчиваем `$0` переход между ними идет `[TAB]`
{{< /bs/alert >}}
#### Чтобы сделать подсказку с заменой пишем

`${1:подсказка}` --- когда начнем ввод, подсказка удалится

#### Зеркалить значения

Очень полезная функция для программирования Latex и Org-mode

```org
\begin{${1:enumerate}}
    $0
\end{$1}
```
Вводим значение в begin, оно автоматически дублируется в end.

#### Собрать в группу в меню

1. В преамбуле каждого сниппета указать `# group: имя группы` у всех одинаковое.
2. Создать директорию с названием группы
3. Поместить в директорию пустой файл с именем ` .yas-make-groups`

#### Добавить в сниппет дату

Просто вставляем функцию, как и любую функцию LISP
```org
`(format-time-string "%Y-%m-%d")`
```
