+++
title = 'Пакет Xcolor и colortbl'
linktitle = ''
date = 2024-11-15T21:12:27+03:00
categories = 'docs'
series = 'latex'
tags = ['color','pdf','documentation']
summary = 'Обзор документации пакетов Xcolor и colortbl'
description = ''
images = ['color.png']
weight = 199
authors = 'ra'
+++

## Установка пакета xcolor

```tex
\usepackage{xcolor}
```
>[!TIP]
>для работы с таблицами можно загрузить пакет `\usepackage{colortbl}` или в объявлении поставить параметр `\usepackage[table]{xcolor}` и в любом случае загрузится `colortbl`

## Цветовые модели

 - `gray`, 
 - `rgb`, 
 - `cmyk`,
 - `natural`, 
 - `cmy`, 
 - `hsb`, 
 - `RGB`, 
 - `HTML`, 
 - `HSB`, 
 - `Gray`
 
## Типовые наборы цветов

 - `dvipsnames`, 
 - `dvipsnames*`, 
 - `svgnames`, 
 - `svgnames*`, 
 - `x11names`, 
 - `x11names*`
 
 ## команда `\xcolorcmd`
 
`\xcolorcmd` выполняет команды пакета над всем документом.
 ```shell
 latex \def\xcolorcmd{\colorlet{black}{red}}\input{a}
 ```
 заменит в документе черный цвет на красный.
 
## Управление цветами

Name| Базовые цвета/нотации | Диапазон значений| По умолчанию  
----|---------------------|----------------|---------
rgb |red, green, blue | [0, 1]<sup>3</sup> | 
cmy |cyan, magenta, yellow| [0, 1]<sup>3 |
cmyk| cyan, magenta, yellow, black| [0, 1]<sup>4</sup> |
hsb |hue, saturation, brightness |[0, 1]<sup>3</sup> | 
Hsb |hue<sup>◦</sup> , saturation, brightness| [0, H] × [0, 1]<sup>2</sup>| H = 360  
tHsb| hue<sup>◦</sup> , saturation, brightness [0, H] × [0, 1]<sup>2</sup>| H = 360  
gray | gray| [0, 1] | 
RGB |Red, Green, Blue| {0, 1, . . . , L}<sup>3</sup>| L = 255  
HTML| RRGGBB| {000000, . . . , FFFFFF}|  
HSB| Hue, Saturation, Brightness| {0, 1, . . . , M }<sup>3</sup>| M = 240 
Gray| Gray| {0, 1, . . . , N }| N = 15  
wave |lambda (nm)| [363, 814]|  

L, M, N --- целые числа; H --- число с плавающей точкой

## Предопределенные цвета

red, green, blue, cyan, magenta, yellow, black, gray, white, darkgray, lightgray, brown, lime, olive, orange, pink, purple, teal, violet.

### загрузка пакетов цветов 
 - dvipsnames/dvipsnames* --- 68 cmyk цветов
 - svgnames/svgnames* --- загрузка 151 rgb цвета.
 - x11names/x11names* загрузка 317 rgb цветов.
 
### \definecolor

`\definecolor [⟨type ⟩]{⟨name ⟩}{⟨model-list ⟩}{⟨spec-list ⟩}` --- определение своего цвета

Варианты определения цвета:
```tex
\definecolor{red}{rgb}{1,0,0},  
\definecolor{red}{rgb/cmyk}{1,0,0/0,1,1,0},  
\definecolor{red}{hsb:rgb/cmyk}{1,0,0/0,1,1,0},  
\definecolor[named]{Black}{cmyk}{0,0,0,1},  
\definecolor{myblack}{named}{Black},
```
 - **type** --- определить свой тип цветовой гаммы
 - **model-list** --- rgb или cmyk или другие
 - **spec-list** --- для rgb это {r,g,b} в диапазоне их значений. Для rgb это от 0 до 1 смотрим таблицу выше 
 
### \providecolor 

`\providecolor [⟨type⟩]{⟨name⟩}{⟨model-list⟩}{⟨spec-list⟩}` --- аналогично \definecolor но только для новых цветов, старые переопределить нельзя

### \colorlet 

`\colorlet [⟨type⟩]{⟨name⟩}[⟨num model ⟩]{⟨color ⟩}` --- переопределяет существующий цвет, например:
```tex
\colorlet{tableheadcolor}{gray!25}
```

## \definecolorset 

`\definecolorset [⟨type⟩]{⟨model-list⟩}{⟨head ⟩}{⟨tail ⟩}{⟨set spec⟩}` --- это очень мощная команда для создания своих наборов цветов. Наверно актуально для создания фирменных цветов и оттенков.

## Стандартные команды управления цветом

### \color 
```tex
\color {⟨color ⟩}  
\color [⟨model-list ⟩]{⟨spec-list ⟩}
```
действует до конца группы {}

