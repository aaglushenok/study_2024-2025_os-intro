---
## Front matter
title: "Этап №6"
subtitle: "Размещение двуязычного сайта на Github."
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

Сделать поддержку английского и русского языков

# Выполнение этапа проекта

В каталоге контент создаем два подкаталога - en, ru, в каждый копируем то, что раньше было в корне

![Создаем каталоги](image/1.png){#fig:001 width=80%}

Теперь от нас требуется разместить элементы сайта на обоих языках - в контенте en перевести посты и проекты на английский язык

![Перевод одного из постов в качестве примера](image/2.png){#fig:002 width=80%}

Также в каждый из каталогов требуется добавить файл конфига (en/ru).yaml

![Файл конфига en.yaml](image/3.png){#fig:003 width=80%}

Теперь наш сайт поддерживает двуязычность и следующий пост пишется сразу на двух языках:

![Пост по прошедшей неделе на английском языке](image/4.png){#fig:004 width=80%}

Также пишем пост на двух языках на тему fedora:

![Пост о федоре на английском языке](image/5.png){#fig:005 width=80%}

Пушим изменения и проверяем работу на хосте:

![Проверяем двуязычность](image/6.png){#fig:006 width=80%}

# Выводы

Мы обновили сайт, добавили двуязычность, теперь наш сайт поддерживает русский и английские языки!

