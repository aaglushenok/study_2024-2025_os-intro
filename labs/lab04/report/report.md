---
## Front matter
title: "Лабораторная работа № 4. Продвинутое использование git."
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

Получение навыков правильной работы с репозиториями git.

# Задание

1. Выполнить работу для тестового репозитория.
2. Преобразовать рабочий репозиторий в репозиторий с git-flow и conventional commits.


# Выполнение лабораторной работы

Установим git-flow из коллекции репозиториев Copr:

![Установка git-flow](image/1.png){#fig:001 width=80%}

Установим Node.js для Fedora:

![Установка Node.js](image/2.png){#fig:002 width=80%}

Настроим Node.js - добавим каталог с исполняемыми файлами, устанавливаемыми yarn, в переменную PATH; 

![Настройка Node.js](image/3.png){#fig:003 width=80%}

Общепринятые коммиты: введем комнады из текста лабораторной работы для помощи в форматировании коммитов, для помощи в создании логов:

![Общепринятые коммиты](image/4.png){#fig:004 width=80%}

Создадим новый репозиторий на GitHub, назовем его git-extended

![Создание репозитория](image/5.png){#fig:005 width=80%}

Рекурсивно клонируем созданный репозиторий. Перейдем в него. Создадим в репозитории файл README.md, запишим в файл слово README, для того чтобы не работать с пустым репозиторием:

![Первый коммит (1)](image/6.png){#fig:006 width=80%}

Пропишем команду git add ., после чего вставим в терминал команды из текста лабораторной работы для первого коммита и отправки файлов:

![Первый коммит (2)](image/7.png){#fig:007 width=80%}

Конфигурация общепринятых коммитов, для пакетов Node.js:

![Конфигурация пакетов](image/8.png){#fig:008 width=80%}

Заполним параметры конфигурационного пакета:

![Заполнение параметров](image/9.png){#fig:009 width=80%}

Добавим новые файлы, выполним коммит, выбирая в окне терминала нужные настройки:

![Добавление файлов, коммит](image/10.png){#fig:010 width=80%}

Отправим файлы на github::

![Отправка файлов на GitHub](image/11.png){#fig:011 width=80%}

Конфигурация git-flow. Инициализируем git-flow, выбирая в окне терминала необходимые параметры. Установим префикс для ярлыков в v.:

![Инициализация git flow; Префикс v](image/12.png){#fig:012 width=80%}

Проверим, что мы на ветке develop. Загрузим весь репозиторий в хранилище:

![Загрузка репозитория в хранилище](image/13.png){#fig:013 width=80%}

Установим внешнюю ветку как вышестоящую для этой ветки. Создадим релиз с версией 1.0.0. Создадим журнал изменений:

![Создание релиза, журнала изменений](image/14.png){#fig:014 width=80%}

Добавим журнал изменений в индекс:

![Добавление журнала изменений в индекс](image/15.png){#fig:015 width=80%}

Зальём релизную ветку в основную ветку. Отправим данные на github. Создадим релиз на github. Для этого будем использовать утилиты работы с github:

![Отправка данных, создание релиза](image/16.png){#fig:016 width=80%}

Создадим ветку для новой функциональности. По окончании разработки новой функциональности следующим шагом следует объединить ветку feature_branch c develop:

![Объединение веток](image/17.png){#fig:017 width=80%}

Создадим релиз с версией 1.2.3. Обновим номер версии в файле package.json. Установим её в 1.2.3.:

![Создание релиза](image/18.png){#fig:018 width=80%}

Создадим журнал изменений. Добавим журнал изменений в индекс:

![Создание журнала изменений](image/19.png){#fig:019 width=80%}

Зальём релизную ветку в основную ветку, с указанием нужных параметров:

![Добавление релизной ветки в основную](image/20.png){#fig:020 width=80%}

Отправим данные на github. Создадим релиз на github с комментарием из журнала изменений:

![Отправка данных, создание релиза](image/21.png){#fig:021 width=80%}

Перейдем на сайт GitHub. Убедимся, что все необходимые файлы успешно созданы:

![Проверка наличия файлов](image/22.png){#fig:022 width=80%}

Убедимя, что все релизы созданы, и номера их версий соответствуют номерам из текста лабораторной работы:

![Проверка релизов](image/23.png){#fig:023 width=80%}

# Выводы

В ходе выполнения лабораторной работы №4 мне удалось приобрести практические навыки правильной работы с репозиториями git.

# Список литературы{.unnumbered}

::: {#refs}
:::
