---
# type: docs 
title: Install HB
date: 2024-11-11T10:48:31+03:00
featured: false
draft: false
comment: true
toc: true
reward: true
pinned: false
carousel: false
series: HUGO
categories: [docs]
tags: [install, blog, soft, framework]
images: [131736.png]
weight: 199
authors:
  - ra
---

Установка и развертывание FrameWork HB HUGO с нуля.

<!--more-->

# Рекомендации к установке
Предварительно установить:

	- Go
	- Последнюю версию Hugo
	- Node.js
	
## Клонируем репозиторий THEME-CARDS

``` shell
git clone --depth 1 https://github.com/hbstack/theme-cards

```

## Копирую структуру сайта в мою директорию

Директорию можно не создавать, она создастся автоматически.

``` shell
cp -r theme-cards/exampleSite mysite
```
## Редактируем `go.mod`

Перейти в директорию сайта (в примере это `mysite`

``` shell
cd mysite
```

Заменить строку в файле `go.mod`

вместо

`module github.com/hbstack/theme-cards/exampleSite`

написать мой репозиторий:

`module github.com/goroedge/dochb`

и удалить директиву replace (когда пишу, строка находится в третьей строчке сверху файла) `replace github.com/hbstack/theme-cards => ../`


Удаляю


## Создать репозиторий

Если его еще нет, то создать на GitHub

## Установить зависимости

В терминале в папке сайта набираем команду:

``` shell
npm ci
```
проверяет текущую версию и может предложить обновиться

мне так и сказал, обновляюсь под правами администратора

``` shell
sudo npm install -g npm@10.9.0
```

пробую еще раз и выполняю `npm audit fix` исправляет ошибки и пробую еще раз.

Небольшая пляска с бубнами по обновлению пакетов npm и вроде все обновилось.

## Запускаем сервер

``` shell
npm run dev

```
Выполняется дозагрузка необходимых модулей и ...

Просит установить `Dart Saas`

https://gohugo.io//functions/css/sass/#dart-sass

Выполнил 

``` shell
sudo pacman -S sass
```
установилось на Manjaro, но выдает сообщения про старость чего-то




Сайт запустился !




## Обновить модули HUGO

``` shell
hugo mod get -u
```
это обновит все модули

