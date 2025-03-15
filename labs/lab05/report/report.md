---
## Front matter
title: "Лабораторная работа № 5. Настройка рабочей среды."
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

Настроить рабочую среду.

# Задание

1. Выполнить работу для тестового репозитория.
2. Преобразовать рабочий репозиторий в репозиторий с git-flow и conventional commits.


# Выполнение лабораторной работы

Установим менеджер паролей pass:

![Установка pass](image/1.png){#fig:001 width=80%}

Установим gopass:

![Установка gopass](image/2.png){#fig:002 width=80%}

Выведем список ключей, инициализируем хранилище: 

![Вывод списка ключей](image/3.png){#fig:003 width=80%}

Созданим ноавый репозиторий pass:

![Создание репозитория](image/4.png){#fig:004 width=80%}

Создадим структуру git, зададим адрес репозитория на хостинге, выполним синхронизацию:

![Создание структуры, синхронизация](image/5.png){#fig:005 width=80%}

Закоммитим и выложим изменения. Проверим статус синхронизации:

![Отправка изменений, проверка](image/6.png){#fig:006 width=80%}

Установим интерфейс для взаимодействия с браузером:

![Установка интерфейса](image/7.png){#fig:007 width=80%}

Установим плагин browserpass:

![Установка плагина](image/8.png){#fig:008 width=80%}

Добавим новый пароль (символ переноса строки), отобразим его для указанного имени файла, заменим существующий пароль :

![Добавление и замена пароля](image/9.png){#fig:009 width=80%}

Установим дополнительное программное обеспечение:

![Установка дополнительного ПО](image/10.png){#fig:010 width=80%}

Установим шрифты:

![Установка шрифтов](image/11.png){#fig:011 width=80%}

Установим бинарный файл с помощью wget. Создадим свой репозиторий для конфигурационных файлов на основе шаблона:

![Установка бинарного файла, создание репозитория](image/12.png){#fig:012 width=80%}

Проверим, что репозиторий создан верно:

![Проверка создания репозитория](image/13.png){#fig:013 width=80%}

Инициализируем chezmoi с нашим репозиторием dotfiles, копируя chezmoi в /usr/local/bin:

![Инициализация chezmoi](image/14.png){#fig:014 width=80%}

Проверим, какие изменения внесёт chezmoi в домашний каталог, согласимя с ними:

![Проверка внесенных изменений](image/15.png){#fig:015 width=80%}

На второй машине инициализируем chezmoi с репозиторием dotfiles через SSH. Проверим, какие изменения внесены и согласимся с ними:

![Использование chezmoi на нескольких машинах](image/16.png){#fig:016 width=80%}

Установим свои dotfiles на новый компьютер с помощью одной команды, извлечем последние изменения из репозитория. Посмотрим, что изменится, фактически не применяя изменения:

![Извлечение последних изменений](image/17.png){#fig:017 width=80%}

Установим автоматическое фиксирование и отправку изменений в исходный каталог в оепозиторий, изменив конфигурационный файл:

![Изменение конфигурационного файла](image/18.png){#fig:018 width=80%}

# Выводы

В ходе выполнения лабораторной работы №5 мне удалось выполнить настройку рабочей среды.

# Список литературы{.unnumbered}

::: {#refs}
:::
