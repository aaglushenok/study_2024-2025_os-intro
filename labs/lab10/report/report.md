---
## Front matter
title: "Лабораторная работа №10. Основы работы с модулями ядра операционной системы"
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

Получить навыки работы с утилитами управления модулями ядра операционной системы.

# Задание  

1. Продемонстрируйте навыки работы по управлению модулями ядра (см. раздел 10.4.1).
2. Продемонстрируйте навыки работы по загрузке модулей ядра с параметрами (см. раздел 10.4.2).

# Выполнение лабораторной работы

## Управление модулями ядра из командной строки

1. Запустите терминал и получите полномочия администратора: su -
2. Посмотрите, какие устройства имеются в вашей системе и какие модули ядра с ними связаны: lspci -k (пояснение: В резльтате вывода мы видим устройства на шине PCI и какие драйверы ядра их используют)

![Задание 1-2](image/1.png){#fig:001 width=80%}

3. Посмотрите, какие модули ядра загружены: lsmod | sort

![Задание 3](image/2.png){#fig:002 width=80%}

4. Посмотрите, загружен ли модуль ext4: lsmod | grep ext4 (нет)
5. Загрузите модуль ядра ext4: modprobe ext4. Убедитесь, что модуль загружен, посмотрев список загруженных модулей: lsmod | grep ext4

![Задание 4-5](image/3.png){#fig:003 width=80%}

6. Посмотрите информацию о модуле ядра ext4:modinfo ext4. Обратите внимание, что у этого модуля нет параметров (Пояснение: В результате вывода мы видим информацию о модуле ядра ext4: имя файла, лицензию, автора и др., а так же видим отсутствие параметров у модуля)

![Задание 6](image/4.png){#fig:004 width=80%}

7. Попробуйте выгрузить модуль ядра ext4: modprobe -r ext4 (пояснение: при первом вводе системы выдает ошибку о том, что модуль находится в использовании. После повторного ввода ошибки нет)
8. Попробуйте выгрузить модуль ядра xfs: modprobe -r xfs  (сообщение об ошибке, поскольку модуль ядра в данный момент используется)

![Задание 7-8](image/5.png){#fig:005 width=80%}

## Загрузка модулей ядра с параметрами

1. Запустите терминал и получите полномочия администратора.
2. Посмотрите, загружен ли модуль bluetooth: lsmod | grep bluetooth
3. Загрузите модуль ядра bluetooth: modprobe bluetooth
4. Посмотрите список модулей ядра, отвечающих за работу с Bluetooth: lsmod | grep bluetooth

![Задание 1-4](image/6.png){#fig:006 width=80%}

5. Посмотрите информацию о модуле bluetooth: modinfo bluetooth (пояснение: 3 модуля, 1 - disable esc, отключает создание eSCO-соединений (для голоса), 2 - disable erti, отключает улучшенный режим повторной передачи (влияет на надежность), 3 - enable ecret, включает улучшенный контроль потока (влияет на стабильность))

![Задание 5](image/7.png){#fig:007 width=80%}

![Задание 5](image/8.png){#fig:008 width=80%}

6. Выгрузите модуль ядра bluetooth: modprobe -r bluetooth

![Задание 6](image/9.png){#fig:009 width=80%}

## Обновление ядра системы

1. Запустите терминал и получите полномочия администратора: su -
2. Посмотрите версию ядра, используемую в операционной системе: uname -r
3. Выведите на экран список пакетов, относящихся к ядру операционной системы: dnf list kernel

![Задание 1-3](image/10.png){#fig:010 width=80%}

4. Обновите систему, чтобы убедиться, что все существующие пакеты обновлены, так как это важно при установке/обновлении ядер Linux и избежания конфликтов: dnf upgrade --refresh

![Задание 4](image/11.png){#fig:011 width=80%}

5. Обновите ядро операционной системы, а затем саму операционную систему: dnf update kernel, dnf update, dnf upgrade --refresh
6. Перегрузите систему. При загрузке выберите новое ядро.

![Задание 5-6](image/12.png){#fig:012 width=80%}

7. Посмотрите версию ядра, используемую в операционной системы: uname -r, hostnamectl (пояснение: версия ядра изменилась с "...570.37.1..." на "...570.58.1...")

![Задание 7](image/13.png){#fig:013 width=80%}

## Контрольные вопросы 

1. Какая команда показывает текущую версию ядра, которая используется на вашей системе?  
uname -r

2. Как можно посмотреть более подробную информацию о текущей версии ядра операционной системы?  
uname -a или посмотреть содержимое /proc/version

3. Какая команда показывает список загруженных модулей ядра?  
lsmod

4. Какая команда позволяет вам определять параметры модуля ядра?  
modinfo имя_модуля

5. Как выгрузить модуль ядра?  
rmmod имя_модуля

6. Что вы можете сделать, если получите сообщение об ошибке при попытке выгрузить модуль ядра?  
Попробовать команду modprobe -r имя_модуля или сначала выгрузить зависимые модули

7. Как определить, какие параметры модуля ядра поддерживаются?  
modinfo имя_модуля или изучить документацию модуля

8. Как установить новую версию ядра?  
Через пакетный менеджер (apt, yum, dnf) или собрать из исходного кода

# Вывод

В ходе выполнения лабораторной работы №10 мне удалось получить навыки работы с утилитами управления модулями ядра операционной системы.

# Список литературы{.unnumbered}

::: {#refs}
:::
