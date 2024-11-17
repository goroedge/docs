---
# type: docs 
title: Titlesec
date: 2024-11-10T09:17:54+03:00
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
images: [101416.png]
---

Оформление стилей страниц, заголовков и оглавления. Продвинутый пакет. Оставляю его для настроек различных стилей документов.

Обзор документации.

<!--more-->
# Пакет TITLESEC
## Подключение пакета

Для установки пакета в преамбуле документа пишем:
```tex
\usepackage[explicit]{titlesec}
```

## Родная документация
https://mirror.macomnet.net/pub/CTAN/macros/latex/contrib/titlesec/titlesec.pdf

## Сам пакет на SPAN 
https://ctan.org/pkg/titlesec


команда `explicit` мне будет нужна, чтобы в настройках заголовков указывать `{#1}` для подстановки в нужное место.

В пакете есть так называемые простые настройки и продвинутые.

# Простые настройки
## Что можно изменять в формате
Для настройки формата заголовка используем три параметра:
1. Тип шрифта `rm sf tt md bf up it sl sc` по умолчанию в заголовках стоит `\bf`.
2. Размер шрифта `big medium small tiny`
3. Выравнивание заголовка `raggedleft center raggedright`
4. `compact` --- задает более компактный вид и уменьшает пробелы
5. `uppercase` --- выведет все буквы заглавными (говорят не всегда работает)

## Основные команды в простом режиме

### titlelabel
`\titlelabel{⟨label-format ⟩}`
Эта команда изменяет формат метки заголовка

```tex
\titlelabel{\thetitle\quad}
```
т.е можно настроить буквенный вывод, изменить длину пробела, поставить точку и т.д.

### titleformat
`\titleformat*{⟨command ⟩}{⟨format⟩}`
Собственно сам формат заголовка.

`command` --- это `\section`, `\subsection` и т.д.

`format` --- соответственно, все, что было сказано выше. Размер шрифта, семейство шрифта и выравнивание.

```tex
\titleformat*{\section}{\Large\sf}
```
Собственно для простой настройки и все!!!

# Продвинутые настройки

## titleformat

```tex
\titleformat{⟨command ⟩}[⟨shape⟩]{⟨format⟩}{⟨label ⟩}{⟨sep⟩}{⟨before-code⟩}[⟨after-code⟩]
```
### command: 
это: 
 - \part, 
 - \chapter, 
 - \section, 
 - \subsection, 
 - \subsubsection, 
 - \paragraph, 
 - \subparagraph.

### shape: 
это:
 - hang --- значение по умолчанию (висящая метка)
 - block --- заголовок помещает в блок. Можно добавлять рисунки и прочее. 
 - display --- помещает метку в отдельный абзац.
 ```tex
 \titleformat{\section}[display] 
{\fontsize{120}{20}\boldfont} 
{\vbox{\hfil\thesection}\hfil}{0em}
{\LARGE\uppercase{#1}}

\titlespacing{\section} {0pc}{20.5ex plus .1ex minus .2ex}{30.5ex minus .1ex}[0pc]
```
![Пример заголовка](101034.png?brightness=-30#center)

Вот так получится. 
 
 - runin --- в документации пишут, что как стандартный параграф, но особо не заметил разницы. Наверно бесполезная вещь.
 
 ```tex
 \titleformat{\subsection}[runin] 
{\fontsize{44}{10}\boldfont} 
{\thesection}{0.5em}
{\LARGE\uppercase{#1}}

\titlespacing{\section} {0pc}{20.5ex plus .1ex minus .2ex}{30.5ex minus .1ex}[0pc]
```
![Образец заголовка](101100.png?brightness=-10#center)
 
 Использую пакет `fontspec` для большей красоты настроек. `fontsize` оттуда.
 
 - leftmargin --- тяжело понять, лучше увидеть. Все выравнивает по левому краю.
 
```tex
\titleformat{\subsection}[leftmargin] 
{\boldfont} 
{\thesection}{1.5em}
{\Large\uppercase{#1}}

\titlespacing{\subsection} {-15pc}{2.5ex plus .1ex minus .2ex}{3.5ex minus .1ex}[5pc]
...

\subsection{Subsection test two line}

```
![Образец заголовка](101112.png?brightness=-10#center)
 
И еще одна интересная заметка для заголовка: если я меняю первый параметр в `\titlespacing` на `3pc` то получится:

![Образец заголовка](101117.png?brightness=-10#center)
 - rightmargin --- как leftmargin, но только вправо. Но у меня результата не получилось. Все улетает за пределы страницы.
 
 titlespasing изменил третий параметр в отрицательную величину, и добился результата.

 
 - drop/wrap --- реально оборачивает текст вокруг заголовка
 ```tex
 \titleformat{\subsection}[wrap] 
{\Large\boldfont} 
{\thesection}{1.5em}
{\uppercase{#1}}

\titlespacing{\subsection}{2pc}{4.5ex plus .1ex minus .2ex}{8.5ex plus .2ex minus .1ex}[2pc]
```
но нужно правильно настроить 3-й параметр в `\titlespacing` я для своего заголовка поставил 8.5ex, в общем подбираем экспериментально. 

Но получилось:
![Образец заголовка](101136.png?brightness=-10#center)

```tex
\titlespacing{\subsection}{12pc}{8.5ex plus .1ex minus .2ex}{8.5ex plus .2ex minus .1ex}[6pc]
```
поменял настройки на 12pc и заголовок стал выглядеть приятнее,
![Образец заголовка](101140.png?brightness=-10#center)
 для сравнения если я поставлю `drop` то будет перенос строк по другому режиму: см. ниже:
![Образец заголовка](101143.png?brightness=-10#center)
 - frame --- также переносит метку в отдельный параграф как display, но еще рисует рамку
 
![Образец заголовка](101150.png?brightness=-10#center)

### format
Все что угодно из латекса. Ставится перед заголовком и действует на метку и заголовок. Цвет, шрифт, размер и пр.

```tex
\titleformat{\section}[display] 
{\color{red}\fontsize{120}{20}\boldfont} 
{\vbox{\hfil\thesection}\hfil}{0em}
{\LARGE\uppercase{#1}}
```
### label

метка раздела. Чтобы все работало корректно лучше ставить, если предусмотрено стилем. Т.к., когда будет применяться команда заголовка со *, то номер подавится автоматически.

```tex
\thesection
\thesubsection
\thesubsubsection
...
```
### sep

отступ от метки. Тоже нельзя оставлять пустым. 0pt но поставь.

### before-code

самая звездная штука. В нее можно поставить вообще все и в качестве аргумента вляпать `#1` как текст заголовка.

```tex
\titleformat{\section} 
{\LARGE\boldfontwhite} 
{}{.5em}
{\colorbox{BleuLBA}{\parbox{21cm}{\rule[-5pt]{0pt}{21pt}\hspace{1.5cm}\thesection\, \uppercase{#1}}}}

```
это я сделал для французов в синей рамочке белыми буквами. Но тут есть одна ошибка. Надеюсь с ней разобраться. Это номер заголовка.

![Образец заголовка](101216.png?brightness=-10#center)

### after-code

тоже самое, что и before, только код ставит после заголовка. Любой!

## chaptertitlename

изменяет название главы по умолчанию

```tex
\renewcommand{\chaptertitlename}{Новое название главы}
```
## titlespacing
```tex
\titlespacing*{⟨command ⟩}{⟨left⟩}{⟨before-sep⟩}{⟨after-sep⟩}[⟨right-sep⟩]
```
Нужная команда для настроек пространства заголовка

Версия со звездочкой убирает отступ абзаца, следующего за заголовком, за исключением случаев удаления, переноса и запуска, где эта возможность не имеет смысла.
### command
команда заголовка \section и т.д.

### left

обязательный параметр, может быть положительный и отрицательный делает отступ заголовка влево и вправо.

Помогает при настройке с параметром `drop` и `wrap`.

### before-sep

буквально вертикаьный отступ перед заголовком

### after-sep

двигает текст после заголовка вертикально и горизонтально. Важен при настройке текста с обтеканием.

### right-sep 

необязательный параметр для установки отступа справа для установок с hang, block и display. Помогает залезать в правое поле.
Это \beforetitleunit и \aftertitleunit тонкие настройки клея в заголовках. Я не использую.

А теперь я добился того, ради чего затевал этот конспект. Я настроил заголовок без ошибок:

```tex
%%%%%%%%%%%%%%% SECTION %%%%%%%%%%%%%5000
\titleformat{\section} [hang]
{\LARGE\boldfontwhite} 
{\llap{\colorbox{BleuLBA}{\parbox{2cm}{\rule[-5pt]{0pt}{21pt}\filleft\thesection}}}}{0em}
{\colorbox{BleuLBA}{\parbox{21cm}{\rule[-5pt]{0pt}{21pt}\filright \uppercase{#1}}}}

\titlespacing{\section} {0pc}{2.5ex plus .1ex minus .2ex}{3.5ex minus .1ex}[0pc]
```

Результат смотрим ниже:
![Образец заголовка](101455.png#center)

### Дополнительные команды выравнивания

`\filright \filcenter \filleft \fillast \filinner \filouter`
в принципе благодаря им очень хорошо настроил и решил свою задачу выше.

Они заполняют пространство перед или после заголовкаа, в зависимости от названия.

`\wordsep` --- пространство между слов в заголовке

`indentafter noindentafter` --- обходит настройки отступов страницы

`rigidchapters rubberchapters` --- регулирует пространство между титулом главы и текстом.

`bottomtitles nobottomtitles nobottomtitles*`

Устанавливаем минимальное пространство внизу страницы, чтобы заголовок не переносился на новую страницу.
```tex
\renewcommand{\bottomtitlespace}{⟨length ⟩}
```

`aftersep largestsep`

По умолчанию, когда есть два последовательных заголовка, между ними используется пространство ⟨after-sep⟩ от первого. Иногда это нежелательное поведение, особенно когда пространство ⟨before-sep⟩ намного больше, чем пространство ⟨after-sep⟩ (в противном случае предпочтительнее выглядит значение по умолчанию). 

`pageatnewline` --- этот странный параметр насильно разрывает заголовок на разные страницы, хотя по умолчанию команды `\\ \\* ` подавлены.

`\nostruts  nostruts` --- подавляет умничество latex при изменении высоты пространства в заголовках.

## RULES

Добавляет линии под заголовками и не только.
```tex
\titleline[⟨align⟩]{⟨horizontal material ⟩} 
\titlerule[⟨height ⟩] 
\titlerule*[⟨width ⟩]{⟨text ⟩}
```
Можно добавить прямо в текст и получить результат для одного заголовка:
```tex
\section{Title first}
\label{sec:title-first}
\titlerule[.8pt]% 
\vspace{1pt}% 
\titlerule
```
или можно эту же конструкцию добавить в настройки `\titleformat`.
![Образец заголовка](101520.png#center)


`calcwidth` --- изменяет формат переноса строк для режима wrap

## PAGE STYLES
```tex
\assignpagestyle{⟨command ⟩}{⟨pagestyle⟩}
...
\assignpagestyle{\chapter}{empty}
```
любой главе или странице можно назначить стиль по умолчанию.

## Breaks

`\sectionbreak \subsectionbreak \subsubsectionbreak \paragraphbreak \subparagraphbreak \⟨section⟩break`

```tex
\newcommand{\sectionbreak}{\clearpage}
или
\newcommand{\sectionbreak}{% 
\addpenalty{-300}% 
\vspace*{0pt}}
```
эта утилита настраивает автоматический разрыв страниц при достижения заданных параметров в разделах.

`\chaptertolists` --- изменяет отступы перед заголовками
```tex
\newcommand{\chaptertolists}{}
```
а этот будет пустой

## Команды в преамбуле

### explicit

позволяет указывать в titleformat #1 как место для текста заголовка
```tex
\titleformat{\section} 
{..} 
{\thesection}{..}{#1.}
```
### newparttoc oldparttoc

используется если \part была переопределена, помогает настроить TOC

### clearempty

Изменяет поведение \cleardoublepage, чтобы на пустых страницах использовался стиль пустой страницы.

### toctitles

Изменяет поведение необязательного аргумента в заголовках разделов, так что он устанавливает только заголовки в квадратных скобках, а не записи оглавления, которые будут основаны на полном заголовке.

### newlinetospace

Заменяет каждое вхождение символов \\ или \\* в заголовках на пробел в заголовках и записях оглавления.

## Расширенные настройки
`⟨key⟩=⟨value⟩, ⟨key⟩=⟨value⟩, ⟨key⟩, ⟨key⟩,...`

Первый аргумент как \titleformat, так и \titlespaceing имеет расширенный синтаксис, который позволяет устанавливать разные форматы в зависимости от контекста.

 - `name=` Допустимые значения: \chapter, \section и т. д. 
 - `page=` Допустимые значения: odd или even.  
 - `numberless` Бесполезный ключ. В этом нет необходимости, если вы не хотите установить разные нумерованные (без этого ключа) и ненумерованные (с безномерными) варианты.
 
 ```tex
\titleformat{name=\section,page=even}[leftmargin]
{\filleft\scshape}{\thesection}{.5em}{} 

\titleformat{name=\section,page=odd}[rightmargin]
{\filright\scshape}{\thesection}{.5em}{}
```
## Создание новыхуровней заголовков

```tex
\titleclass{⟨name ⟩}{⟨class ⟩}  \titleclass{⟨name⟩}{⟨class⟩}[⟨super-level-cmd ⟩]
```

Существует три класса: 
 - `page` — это часть книги, на одной странице, 
 - `top` — это \chapter, который начинает страницу и помещает заголовок вверху,
 - `straight` предназначен для заголовков в середине текста.

В первом случае `\titleclass{\part}{straight}` заменяется просто класс.

Во втором случае, можно создать новые подуровни:
```tex
\titleclass{\subchapter}{straight}[\chapter] %новый класс
\newcounter{subchapter} %новый счетчик
\renewcommand{\thesubchapter}{\Alph{subchapter}} %буквенный счетчик
```

уровни секций изменяются автоматически

Глава 0 -- уровень
\section --- 1 уровень и т.д.

### loadonly

Обнулит все настройки уровней и позволит создавать свои уровни с нуля.

### \titleclass
```tex
\titleclass{⟨name ⟩}[⟨start-level-num ⟩]{⟨class ⟩}
```
добавляет высшего уровня заголовок (0) или (-1) и дальше создаем сои новые уровни.

## FootNotes

В заголовки можно добавлять ссылки `footnotes`, но чтобы они не показывались в оглавлении нужно в преамбулу добавить:
```tex
\usepackage[stable]{footmisc}
```
### Номер заголовка в BOX

Полезная вещь. Особенно когда колдуешь с отступами за пределы печатаемой области или работаешь с цветами.

```tex
\titleformat{\section} 
{..} 
{\makebox[2em]{\thesection}}{..}{..}

или

\titleformat{\section} [hang]
{\LARGE\boldfontwhite} 
{\llap{\colorbox{BleuLBA}{\parbox{2cm}{\rule[-5pt]{0pt}{21pt}\filleft\thesection}}}}{0em}
{\colorbox{BleuLBA}{\parbox{21cm}{\rule[-5pt]{0pt}{21pt}\filright \uppercase{#1}}}}

```

### Подавляет нумерацию заголовков
```tex
\setcounter{secnumdepth}{0}

или

\newenvironment{exercises} 
{\setcounter{secnumdepth}{0}} 
{\setcounter{secnumdepth}{2}}

или

\newenvironment{exercises} 
{\setcounter{secnumdepth}{0}%
\addtocontents{toc}{\protect\setcounter{tocdepth}{0}\ignorespaces}} 

{\setcounter{secnumdepth}{2}%
\addtocontents{toc}{\protect\setcounter{tocdepth}{2}\ignorespaces}}
```

### Как пометить заголовки со сзвездочкой
```tex
\newcommand{\secmark}{} 
	\newenvironment{advanced} 
		{\renewcommand{\secmark}{*}} 
		{} 
\titleformat{\section} {..} 
{\thesection\secmark\quad}{..}{..}  

В документе пишим  

\begin{advanced} 
\section{...} ... 
\end{advanced}
```

Этот раздел будет со звездочкой.


## Крутой код по настройке стилей страниц
```tex
\documentclass[14pt,a4paper,twoside]{extbook}
\usepackage[utf8]{inputenc} %
\usepackage[T1]{fontenc}
\usepackage{lmodern} %
\usepackage[pagestyles]{titlesec}
\usepackage[x11names]{xcolor} %
\usepackage{theorem}
\newtheorem{worked example}{Worked Example}[chapter]
\newtheorem{solution}{SOLUTION}[chapter]
%\usepackage{anyfontsize}
\usepackage{amsfonts}
\usepackage{textcomp}
\usepackage{enumerate}
\setlength\headheight{21pt}

\newcommand{\hsp}{\hspace{20pt}}
\newcommand{\ntl}{\newline \newline}

\titleformat{\chapter}[hang]{\fontsize{50}{60}\bfseries\color[rgb]{0,0.5,0.75}}{\thechapter\hsp\fontsize{90}{60}\selectfont\textcolor{black}{|}\hsp}{0pt}{\thispagestyle{empty}\Huge\bfseries}

\titleformat{\section}{\large\bfseries}{}{0pt}{\textcolor[rgb]{0,0.5,0.75}{Topic \thesection} \ }[{\titlerule[0.8pt]}]

\usepackage{blindtext}

\newpagestyle{mine}{%
\setlength\fboxsep{10pt}
\sethead[\bfseries\llap{\colorbox{SteelBlue3}{\parbox{\dimexpr\marginparsep + \marginparwidth\relax}{\hspace{20pt}\color{white}\thepage\vphantom{|}}}}%
\colorbox{SlateGray2!40}{\parbox{\dimexpr\linewidth-2\fboxsep}{~\thechapter~|\hspace{0.75em}\chaptertitle}}][][]%
{}{}{\bfseries\colorbox{SlateGray2!40}{\parbox{\dimexpr\linewidth-2\fboxsep}{\thesection~|\hspace{0.75em}\sectiontitle}}%
\rlap{\colorbox{SteelBlue3}{\parbox{\dimexpr\marginparsep + \marginparwidth\relax}{\hspace{20pt}\color{white}\thepage\vphantom{|}}}}}
\setfoot{}{}{}
}

\pagestyle{mine}

\begin{document}

\chapter{{NUMBER}}%\textcolor{black}
\section{BIDMAS.}
\blindtext[10]

\end{document} 
```

Выдает шикарную вещь: 
![Образец заголовка](101416.png?#center)
