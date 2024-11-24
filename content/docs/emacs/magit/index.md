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
authors:
  - ra
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
![Left](magit.png?width=400px#float-start)
`s` / `u` добавить файл в индекс или убрать из индекса.  
`C-SPC` --- поставить метку на файле `C-n` `C-p` отметить список файлов из отменить,потом `s` или `u` для включения или исключения.  
`c` <mark>откроет</mark> меню для COMMIT и другие варианты, нажимаю еще раз `c`, ввожу комментарий commit  и нажимаю `C-c` для выполнения commit. 

Key             Binding

TAB		magit-section-toggle
RET		magit-visit-thing
C-w		magit-copy-section-value
SPC		magit-diff-show-or-scroll-up
!		magit-run
$		magit-process-buffer
%		magit-worktree
+		magit-diff-more-context
-		magit-diff-less-context
0		magit-diff-default-context
1		magit-section-show-level-1
2		magit-section-show-level-2
3		magit-section-show-level-3
4		magit-section-show-level-4
5 .. 9		digit-argument
:		magit-git-command
<		beginning-of-buffer
>		magit-sparse-checkout
?		magit-dispatch
A		magit-cherry-pick
B		magit-bisect
C		magit-clone
D		magit-diff-refresh
E		magit-ediff
F		magit-pull
G		magit-refresh-all
H		magit-describe-section
I		magit-init
J		magit-display-repository-buffer
K		magit-file-untrack
L		magit-log-refresh
M		magit-remote
O		magit-subtree
P		magit-push
Q		magit-git-command
R		magit-file-rename
S		magit-stage-modified
T		magit-notes
U		magit-unstage-all
V		magit-revert
W		magit-patch
X		magit-reset
Y		magit-cherry
Z		magit-worktree
^		magit-section-up
a		magit-cherry-apply
b		magit-branch
c		magit-commit
d		magit-diff
e		magit-ediff-dwim
f		magit-fetch
g		magit-refresh
h		magit-dispatch
i		magit-gitignore
j		magit-status-jump
k		magit-delete-thing
l		magit-log
m		magit-merge
n		magit-section-forward
o		magit-submodule
p		magit-section-backward
q		magit-mode-bury-buffer
r		magit-rebase
s		magit-stage-file
t		magit-tag
u		magit-unstage-file
v		magit-revert-no-commit
w		magit-am
x		magit-reset-quickly
y		magit-show-refs
z		magit-stash
DEL		magit-diff-show-or-scroll-down
S-SPC		magit-diff-show-or-scroll-down
C-<return>	magit-visit-thing
C-<tab>		magit-section-cycle
M-<tab>		magit-section-cycle-diffs
<backtab>	magit-section-cycle-global

<remap> <dired-jump>	magit-dired-jump

<remap> <back-to-indentation>	magit-back-to-indentation
<remap> <evil-next-line>	evil-next-visual-line
<remap> <evil-previous-line>	evil-previous-visual-line
<remap> <next-line>		magit-next-line
<remap> <previous-line>		magit-previous-line

C-c C-c		magit-dispatch
C-c C-e		magit-edit-thing
C-c C-o		magit-browse-thing
C-c C-w		magit-copy-thing

C-M-i		magit-dired-jump
M-w		magit-copy-buffer-revision

C-c TAB		magit-section-cycle

M-1		magit-section-show-level-1-all
M-2		magit-section-show-level-2-all
M-3		magit-section-show-level-3-all
M-4		magit-section-show-level-4-all
M-n		magit-section-forward-sibling
M-p		magit-section-backward-sibling

<left-fringe> <mouse-1>	magit-mouse-toggle-section
<left-fringe> <mouse-2>	magit-mouse-toggle-section


In addition to any hooks its parent mode ‘magit-mode’ might have run,
this mode runs the hook ‘magit-status-mode-hook’, as the final or
penultimate step during initialization.
