---
# type: docs 
title: Pdfpages
date: 2024-11-10T20:03:51+03:00
featured: false
draft: false
comment: true
toc: true
reward: true
pinned: false
carousel: false
series: latex
categories: [docs]
tags: [pdf]
images: [adobe.png]
---

Вдруг понадобилось вставить титульную страницу, сделанную на XARA. Пришлось подключить пакет `pdfpages`

<!--more-->

# Пакет PDFPAGES
## Подключение пакета

Для установки пакета в преамбуле документа пишем:
```tex
\usepackage[⟨options ⟩]{pdfpages}
```

## Родная документация
https://mirror.macomnet.net/pub/CTAN/macros/latex/contrib/pdfpages/pdfpages.pdf

## Сам пакет на SPAN 
https://ctan.org/pkg/pdfpages

## Опции при подключении

⟨option⟩ 
 – final: режим по умолчанию, вставляет страницы в документ
 - draft: не вставляет страницу, но вставляет ссылку в боксе  
 - demo: вставляет пустую страницу 
 - nodemo: отключает демо
 
 ## Вставка документа
 
 ```tex
 \includepdf[⟨key=val ⟩]{⟨filename⟩}
 ```
 Вставляет файл где укажешь.
 
 Key=val могут быть различными.
 
 Если нужно вставить избранные страницы, используем ключ `page`
 ```tex
pages={3,5,6,8})
pages={4-9}
pages={3,{},8-11,15}
```

`nup` --- укладывает логические страницы на лист (что-то вроде микространиц) `nup=⟨xnup⟩x⟨ynup⟩`

`landscape=false` --- по умолчанию, но можно развернуть, если нужно

и еще куча всяких опций для какого-то боловства. Мне пока хватает этого.

