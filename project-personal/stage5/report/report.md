---
## Front matter
title: "Этап №5"
subtitle: "Добавляем остальные элементы на сайт"
author: "Анна Александровна Глушенок"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Добавить на сайт записи проектов, пост по прошедшей неделе, добавить пост на тему по языки научного программирования

# Выполнение этапа проекта

В каталоге content - project создаем новые папки, каждая из которых будет являтся проектом

![Создаем каталоги](image/1.png){#fig:001 width=80%}

В каждой из папок добавляем аватарку проекта и редактируем файл index

![Аватарка и файл index](image/2.png){#fig:002 width=80%}

Редактирование index:

![Добавляем свой проект](image/3.png){#fig:003 width=80%}

Те же действия для другого проекта:

![Добавляем свой проект](image/4.png){#fig:004 width=80%}

Те же действия для другого проекта:

![Добавляем свой проект](image/5.png){#fig:005 width=80%}

Также делаем пост по прошедшей неделе(4th week):

![Пост](image/6.png){#fig:006 width=80%}

Добавляем пост на тему "Языки научного программирования":

![Пост](image/7.png){#fig:007 width=80%}

Обновляем изменения с помощью hugo server и смотрим на локальном хосте:

![Пост](image/8.png){#fig:008 width=80%}

# Выводы

Мы обновили сайт, добавили проекты, сделали пост по прошедшей неделе,добавили пост на тему языки научного программирования

