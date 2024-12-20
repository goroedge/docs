+++
title = 'HUGO Icon'
linktitle = 'Icons'
date = 2024-11-15T11:47:35+03:00
categories = 'docs'
series = 'hugo'
tags = ['documentation', 'soft']
summary = 'Настройка иконок в HUGO'
description = ''
images = ['151358.png']
weight = 199
authors = 'ra'
+++
## Используем библиотеку AWESOME

https://fontawesome.com/

Просто переходим по ссылке и выбираем нужную иконку

### Меню Releart
Для отображения в меню для темы `Relearn` в front matter нужно добавить запись

```toml
menuPre = '<i class="fas fa-icons"></i> '
```
где, `fas` --- это класс AWESOME, `fa-` перед названием иконки, название иконки.

Все,иконка появится перед начертанием меню.

`fab`--- для обозначения брендов.

### Иконка в тексте
```go
Built with {{ icon heart }} by Relearn and Hugo
```
![AWESOME](151358.png ) 
Здесь просто имя из каталога AWESOME и получим: 
Этот вариант работает под темой Revalart
Built with {{ icon heart }} by Relearn and Hugo

Или через class

```html
Built with <i class="fas fa-heart"></i> by Relearn and Hugo
```

В HUGO.toml добавить настройку
```toml
[markup.goldmark.renderer]
    unsafe = true
```

## Подключение своих SVG

### Версия 1

1. Создаю директорию `svg` в корне проекта. В надежде, что мои SVG не будут копироваться в Public

2. Создаю файл: `layout/sgortcodes/svg/html`
```html
<figure class="{{index .Params 1}}">
  {{ readFile (print "svg/" (index .Params 0)) | safeHTML }}
</figure>
```
3. Кидаю свои `svg` файлы в папку `/svg/`

4. Вызываю из markdown командой `{{ svg имя-файла.svg}}` и все!!!!
{{% svg rect.svg %}}
{{% svg rect1.svg %}}

## Смертельный номер!!!
просто беру и вставляю tag `svg` со всем содержимым в markdown
и вообще все!
```html
<svg
   width="110.80958mm"
   height="85.746887mm"
   viewBox="0 0 110.80958 85.746887"
   version="1.1"
   id="svg1"
   xmlns="http://www.w3.org/2000/svg"
   xmlns:svg="http://www.w3.org/2000/svg">
  <defs
     id="defs1" />
  <g
     id="layer1"
     transform="translate(-53.4722,-58.53525)">
    <rect
       style="fill:#45c1e9;stroke-width:0.499999"
       id="rect1"
       width="80.608917"
       height="64.65387"
       x="53.472202"
       y="58.535252" />
    <ellipse
       style="fill:#ff0000;stroke-width:0.499999"
       id="path1"
       cx="126.27881"
       cy="113.2809"
       rx="38.002975"
       ry="31.001232" />
  </g>
</svg>
```
Как например эту козявку: <svg
   width="4.0472617mm"
   height="4.1428432mm"
   viewBox="0 0 4.0472617 4.1428432"
   version="1.1"
   id="svg1"
   xmlns="http://www.w3.org/2000/svg"
   xmlns:svg="http://www.w3.org/2000/svg">
  <defs
     id="defs1" />
  <g
     id="layer1"
     transform="translate(-51.75966,-93.015149)">
    <path
       style="fill:#ff0000;stroke-width:0.020124"
       d="m 52.629401,94.54504 c -1.573658,0.148998 -0.553055,2.165001 -0.443567,2.215367 0.974867,0.448449 1.525568,0.508369 2.068476,0.225967 0.08044,-0.04184 1.559891,-3.139455 1.552585,-3.290399 -0.0073,-0.150943 -0.807251,0.469465 -0.872001,0.469465 -0.06475,0 -1.145357,1.660859 -1.145357,1.660859 0,0 -1.793211,0.45894 -0.63511,-0.449772 0.25578,-0.2007 0.949535,-1.136581 0.923818,-1.25266 -0.02572,-0.116078 -0.939717,0.292737 -0.939717,0.292737 0,0 -0.530625,-1.471988 -0.625499,-1.398816 -0.09487,0.07317 0.116372,1.527252 0.116372,1.527252 z"
       id="path2" />
  </g>
</svg>
Это был просто полигон
<svg height="210" width="500">
  <polygon points="200,10 250,190 160,210" style="fill:lime;stroke:purple;stroke-width:1" />
</svg>

А это обычный файл из `inkscape`
<svg
   width="4.0472617mm"
   height="4.1428432mm"
   viewBox="0 0 4.0472617 4.1428432"
   version="1.1"
   id="svg1"
   xmlns:inkscape="http://www.inkscape.org/namespaces/inkscape"
   xmlns:sodipodi="http://sodipodi.sourceforge.net/DTD/sodipodi-0.dtd"
   xmlns="http://www.w3.org/2000/svg"
   xmlns:svg="http://www.w3.org/2000/svg">
  <sodipodi:namedview
     id="namedview1"
     pagecolor="#ffffff"
     bordercolor="#000000"
     borderopacity="0.25"
     inkscape:showpageshadow="2"
     inkscape:pageopacity="0.0"
     inkscape:pagecheckerboard="0"
     inkscape:deskcolor="#d1d1d1"
     inkscape:document-units="mm" />
  <defs
     id="defs1" />
  <g
     inkscape:label="Слой 1"
     inkscape:groupmode="layer"
     id="layer1"
     transform="translate(-51.75966,-93.015149)">
    <path
       style="fill:#ff0000;stroke-width:0.020124"
       d="m 52.629401,94.54504 c -1.573658,0.148998 -0.553055,2.165001 -0.443567,2.215367 0.974867,0.448449 1.525568,0.508369 2.068476,0.225967 0.08044,-0.04184 1.559891,-3.139455 1.552585,-3.290399 -0.0073,-0.150943 -0.807251,0.469465 -0.872001,0.469465 -0.06475,0 -1.145357,1.660859 -1.145357,1.660859 0,0 -1.793211,0.45894 -0.63511,-0.449772 0.25578,-0.2007 0.949535,-1.136581 0.923818,-1.25266 -0.02572,-0.116078 -0.939717,0.292737 -0.939717,0.292737 0,0 -0.530625,-1.471988 -0.625499,-1.398816 -0.09487,0.07317 0.116372,1.527252 0.116372,1.527252 z"
       id="path2"
       sodipodi:nodetypes="csssscsscsc"
       inkscape:export-filename="path3.svg"
       inkscape:export-xdpi="96"
       inkscape:export-ydpi="96" />
  </g>
</svg>

## BootStrap

Установка иконок в Bootstrap

```yaml
module:
  imports:
  - path: github.com/hugomods/icons/vendors/bootstrap
  - path: github.com/hugomods/icons/vendors/font-awesome```
```
