---
# type: docs 
title: Titleps
date: 2024-11-10T17:25:40+03:00
featured: false
draft: false
comment: true
toc: true
reward: true
pinned: false
carousel: false
series: Latex
categories: [docs]
tags: [TOC, pagestyle, title]
images: [131227.png]
weight: 199
authors:
  - ra
---

Оформление стилей страниц, заголовков и оглавления. Продвинутый пакет. Оставляю его для настроек различных стилей документов.

Совместно с TITLESEC бомбическая штука по настройке стилей страниц.
Обзор документации.

<!--more-->
# Пакет TITLEPS
## Установка пакета
Для установки пакета в преамбуле документа пишем:
```tex
\usepackage[pagestyles]{titlesec}
```

### Страница репозитория
https://ctan.org/pkg/titleps

### Документация
https://mirror.truenetwork.ru/CTAN/macros/latex/contrib/titlesec/titleps.pdf

## Определение стиля страницы

``` tex
\newpagestyle{⟨name⟩}[⟨global-style⟩]{⟨commands⟩} 

\renewpagestyle{⟨name⟩}[⟨global-style⟩]{⟨commands⟩}
```

Они их почему-то называют верхние и нижние команды.

### Установка для HEADER и FOOTER
``` tex
\sethead[⟨even-left⟩][⟨even-center⟩][⟨even-right⟩] {⟨odd-left⟩}{⟨odd-center⟩}{⟨odd-right⟩}

\setfoot[⟨even-left⟩][⟨even-center⟩][⟨even-right⟩] {⟨odd-left⟩}{⟨odd-center⟩}{⟨odd-right⟩}
```

А теперь по-порядку.

Все <even> --- т.е четные, это не обязательные параметры, а <odd> --- обязательные.

<even-left> --- верх левый четной страницы.

#### Первая группа комманд
	– \thechapter, \thesection, \thesubsection. . . --- печатают номера заголовков
	– \chaptertitle, \sectiontitle, \subsectiontitle. . . --- печатают наименования заголовков  
	– (только для titlesec) \ifthechapter{⟨true⟩}{⟨false⟩}, \ifthesection{⟨true⟩}{⟨false⟩}, \ifthesubsection{⟨true⟩}{⟨false⟩}. . . --- проверяют где сейчас находится страница  
	– любые другие команды
	
#### Вторая группа комманд

относится ко всему, что есть на странице:
	- \thepage
	- другие не включенные в первую группу
	
### Установка MARKSов

``` tex
\settitlemarks{⟨level-name⟩,⟨sublevel-name⟩,⟨subsublevel-name⟩...}

\settitlemarks*{⟨level-name⟩,⟨sublevel-name⟩,⟨subsublevel-name⟩...}
```

Устанавливает, какие команды \...title должны быть определены и когда выдаются метки; допускается любое количество уровней (1, 2, 3...). Например, `\settitlemarks{chapter,section}`

### Установка RULES

``` tex
\headrule 
\footrule 
\setheadrule{⟨length⟩} 
\setfootrule{⟨length⟩}
```
линии будут проведены под или над калантитулом

### Установка отступов RULES

``` tex
\makeheadrule 
\makefootrule

\renewcommand{\makeheadrule}{\rule[-.3\baselineskip]{\linewidth}{⟨dim⟩}}
```

Этот пример из документации создаст две линнии в HEADER 

``` tex
\renewcommand{\makeheadrule}{% 
\makebox[0pt][l]{\rule[.7\baselineskip]{\linewidth}{0.8pt}}% 
\color[named]{Red}% 
\rule[-.3\baselineskip]{\linewidth}{0.4pt}}
```

## \markboth and \markleft

В документации целая дискуссия по поводу не нужности \markboth и что достаточно \markleft.

Пока не вдаюсь в подробности, но в пакете есть функция `\setmarkboth{⟨code-to-use⟩}`, чтобы переопределить markboth.

## Headline/footline ширина

``` tex
\widenhead[⟨even-left⟩][⟨even-right⟩]{⟨odd-left⟩}{⟨odd-right⟩}

\widenhead*{⟨even-right/odd-left⟩}{⟨even-left/odd-right⟩}
```

Этот параметр соответственно добавляет ширину header и footer-ов.

``` tex
\widenhead*{0pt}{6pc}
тоже самое
\widenhead[6pc][0pt]{0pt}{6pc}
```

`nopatches` --- это опция в преамбуле пакета для самостоятельной тонкой настройки с помощью `\sectionmark`.


## Marks

Марксы можно получить 4 способами:

	- top marks 
	- first marks 
	- botttom marks 
	- next top marks
