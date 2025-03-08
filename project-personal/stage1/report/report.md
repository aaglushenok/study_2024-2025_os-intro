---
## Front matter
title: "Выполнение индивидуального проекта. Стадия 1."
subtitle: "Отчет"
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

Размещение на Github pages заготовки для персонального сайта.

# Задание

1. Установить необходимое программное обеспечение.
2. Скачать шаблон темы сайта.
3. Разместить его на хостинге git.
4. Установить параметр для URLs сайта.
5. Разместить заготовку сайта на Github pages.

# Выполнение индивидуального проекта

Скачаем hugo sites с github:

![Скачивание hugo sites (1)](image/1.png){#fig:001 width=80%}

![Скачивание hugo sites (2)](image/2.png){#fig:002 width=80%}

Распакуем установленный ахив, переместим файл hugo в каиалог /usr/local/bin:

![Распаковка архива, перемещение hugo](image/3.png){#fig:003 width=80%}

На ТУИСе перейдем в раздел "Техническая реализация проекта", перейдем по ссылке на репозиторий с необходимыми файлами. Нажмем "use this template" -> "create new repository", создав новый репозиторий по заданному шаблону:

![Переход к шаблону](image/4.png){#fig:004 width=80%}

![Создание репозитория по шаблону](image/5.png){#fig:005 width=80%}

Зададим имя нового репозитория website (далее изменен на "blog"):

![Ввод имени репозитория](image/6.png){#fig:006 width=80%}

Клонируем созданный репозиторий в папку work:

![Клонирование репозитория](image/7.png){#fig:007 width=80%}

Скачаем go через sudo dnf install go:

![Скачивание go](image/8.png){#fig:008 width=80%}

Перейдем в каталог website и введем hugo server, после чего сайт "соберется", и в терминале мы получим ссылку и номер порта для открытия сайта. После перехода по ссылке видим открывшийся сайт:

![Сборка сайта](image/9.png){#fig:009 width=80%}

Создадим еще один новый репозиторий, зададим его имя как "aaglushenok.github.io:

![Создание 2-го нового репозитория](image/10.png){#fig:010 width=80%}

![Именование репозитория](image/11.png){#fig:011 width=80%}

Клонируем 2-ой созданный репозиторий в папку work. Перейдем в папку с материалами репозитория. Использую "git checkout -b main" переключимся на новую ветку main:

![Клонирование репозитория, переход на ветку main](image/12.png){#fig:012 width=80%}

Для того чтобы не работать с пустым репозиторием, создадим фиктивный файл README.md. Пропишем команду git add ., выполним коммит.

![Выполнение коммита](image/13.png){#fig:013 width=80%}

Перейдем в каталог blog (бывш. website), удалим файл public. Добавим submodule:

![Добавление submodule, удаление public](image/14.png){#fig:014 width=80%}

Повторно пропишем hugo, после "сборки" сайта убедимя, что puplic удален, затем введем "git remote -v" :

![Повторная сборка; Проверка удаления public](image/15.png){#fig:015 width=80%}

Введем команду git add ., выполним коммит. Пропишем команду git push для отправки файлов, с указанием ветки origin main:

![Выполнение коммита](image/16.png){#fig:016 width=80%}

![Отправка файлов](image/17.png){#fig:017 width=80%}

Откроем репозиторий на github, убедимя, что он заполнен всеми необходимыми файлами:

![Проверка наличия файлов](image/18.png){#fig:018 width=80%}

Копируем имя репозитория, введем его в виде ссылки в FireFox. Убедимся, что по введенной ссылке открывается наш сайт:

![Копирование имени репозитория](image/19.png){#fig:019 width=80%}

![Открытие сайта по ссылке](image/20.png){#fig:020 width=80%}

# Выводы

В ходе выполнения первой стадии индивидуального проекта мне удалось разместить на Github pages заготовки для персонального сайта.

# Список литературы{.unnumbered}

::: {#refs}
:::
