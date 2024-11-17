---
# type: docs 
title: Как настроить и работать с Magit?
slug: magit-setup
date: 2024-10-26T12:51:54+03:00
featured: false
draft: false
comment: true
toc: true
reward: true
pinned: false
carousel: false
series: emacs
categories: docs
tags: [magit, emacs]
images: [logo2.png]
---

Настройка Magit в Emacs и управление репозиторием.

<!--more-->


# Введение
Magit - это интерфейс к системе управления версиями Git, реализованный как пакет Emacs.

Магит обертывает и во многих случаях улучшает по крайней мере следующий Git команды: `add`, `am`, `bisect`, `blame`, `branch`, `checkout`, `cherry`, `cherry-pick`, `clean`, `clone`, `commit`, `config`, `describe`, `diff`, `fetch`, `format-patch`, `init`, `log`, `merge`, `merge-tree`, `mv`, `notes`, `pull`, `rebase`, `reflog`, `remote`, `request-pull`, `reset`, `revert`, `rm`, `show`, `stash`, `submodule`, `subtree`, `tag` и `worktree`.

# Установка {class = ".skype-icon"}
Magit может быть установлен с помощью менеджера пакетов Emacs’ или вручную из его репозиторий разработки.

1. В файл конфигурации init.el добавить следующие две строки для доступа к репозиториям.
Установка из Melpa:
```emacs
(require 'package)
(add-to-list 'package-archives
             '("melpa" . "https://melpa.org/packages/") t)
```
Установка из Melpa-Stable:
```emacs
(require 'package)
(add-to-list 'package-archives
             '("melpa-stable" . "https://stable.melpa.org/packages/") t)
```

2. Выполнить команду
```emacs
M-x package-install RET magit RET
```

3. Проверим установку Magit
```emacs
M-x magit-version RET

```
Сообщение: `Magit 20241010.1930 [>= 20241010.1930], Transient 20241009.1745, Git 2.46.1, Emacs 29.4, gnu/linux`
подтвердит установку.

# Команды Magit
`C-x g` для отображения информации о текущем репозитории Git  
![Left](/images/magit.png?width=400px#float-start)
`s` / `u` добавить файл в индекс или убрать из индекса.  
`C-SPC` --- поставить метку на файле `C-n` `C-p` отметить список файлов из отменить,потом `s` или `u` для включения или исключения.  
`c` <mark>откроет</mark> меню для COMMIT и другие варианты, нажимаю еще раз `c`, ввожу комментарий commit  и нажимаю `C-c` для выполнения commit. 

