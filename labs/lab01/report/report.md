---
## Front matter
title: "Лабораторная работа №1. Установка и конфигурация
операционной системы на виртуальную машину."
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

Целью данной работы является приобретение практических навыков установки операционной системы на виртуальную машину, настройки минимально необходимых для дальнейшей работы сервисов.

# Выполнение лабораторной работы

Скачиваем с сайта разработчика DVD-образ операционной системы, соответствующий архитектуре моего компьютера (версия 9.6).

![Скачивание DVD-образа](image/1.png){#fig:001 width=80%}

Открываем VirtualBox, и нажимаем "создать" для создания новой виртуальной машины.

![Создание новой ВМ](image/2.png){#fig:002 width=80%}

В разделе "Имя и тип ОС" задаем имя виртуальной машины (Rocky), образ диска ISO, а так же пропускаем автоматическую установку.

![Имя и тип ОС](image/3.png){#fig:003 width=80%}

В разделе "Оборудование" выделяем основную память (4096 МБ) и процессоры (4).

![Оборудование](image/4.png){#fig:004 width=80%}

В разделе "Жесткий диск" создаем новый виртуальный жесткий диск, и выделяем на систему 30 ГБ.

![Жесткий диск](image/5.png){#fig:005 width=80%}

Далее выбираем "Install Rocky 9.6" и запускаем установку ВМ.

![Установка ВМ](image/6.png){#fig:006 width=80%}

Затем выбираем язык интерфейса ОС. 

![Выбор языка интерфейса ОС](image/7.png){#fig:007 width=80%}

Приступаем к настройке установки. Для начала выбираем место установки.

![Место установки](image/8.png){#fig:008 width=80%}

Далее отключаем KDUMP.

![Отключение KDUMP](image/9.png){#fig:009 width=80%}

Меняем имя узла: устанавливаем aaglushenok.localdomain.

![Имя узла](image/10.png){#fig:010 width=80%}

Устанавливаем пароль root, разрешение на ввод пароля при использовании ключа SSH.

![Пароль root](image/11.png){#fig:0011 width=80%}

Создаем пользователя (aaglushenok), делаем его администратором.

![Создание пользователя](image/12.png){#fig:012 width=80%}

Запускаем установку ОС. Заходим в ОС под заданной учетной записью.

![Вход в ОС](image/13.png){#fig:013 width=80%}

Подключаем образ диска дополнений гостевой ОС.

![Подключение образа диска гостевой ОС](image/14.png){#fig:014 width=80%}

![Загрузка дополнений](image/15.png){#fig:015 width=80%}

Перезапускаем ВМ.

![Перезапуск ВМ](image/16.png){#fig:016 width=80%}

Пункт "установка имени пользователя и названия хоста" из материалов к ЛР пропускаем, тк все подпункты уже выполнены.

# Домашнее задание 

1. Смотрим вывод команды dmesg | less.

![Ввод команды dmesg | less](image/17.png){#fig:017 width=80%}

![Вывод команды dmesg | less](image/18.png){#fig:018 width=80%}

2. Узнаем версию ядра Linux.

![Версия ядра Linux](image/19.png){#fig:019 width=80%}

3. Узнаем частоту процессора.

![Частота процессора](image/20.png){#fig:020 width=80%}

4. Узнаем модель процессора.

![Модель процессора](image/21.png){#fig:021 width=80%}

5. Узнаем объем достпной оперативной памяти.

![Объем доступной оперативной памяти](image/22.png){#fig:022 width=80%}

6. Узнаем тип обнаруженного гипервизора.

![Тип обнаруженного гипервизора](image/23.png){#fig:023 width=80%}

7. Узнаем тип файловой системы корневого раздела и последовательность монтирования файловых систем.

![Тип файловой системы и последовательность монтирования](image/24.png){#fig:024 width=80%}

# Выводы

В ходе выполнения лабораторной работы №1 мне удалось приобрести практические навыки установки операционной системы на виртуальную машину, настройки минимально необходимых для дальнейшей работы сервисов.

# Контрольные вопросы

1. Команды терминала и примеры:
*   Справка: man <команда> (пример: man ls), <команда> --help (пример: ls --help).
*   Перемещение: cd <путь> (пример: cd /home/user/Documents), cd .., cd ~.
*   Просмотр содержимого: ls (по умолчанию), ls -l, ls -a.
*   Определение объёма: du -sh <каталог> (пример: du -sh Documents).
*   Создание/удаление: mkdir <имя>, rmdir <имя>/rm -r <каталог>, touch <имя>, rm <имя>.
*   Права доступа: chmod <права> <файл>, chown <пользователь>:<группа> <файл>.
*   История команд: history, !123.

2. Учётная запись пользователя и команды просмотра:
*   Информация: Имя, UID, GID, домашний каталог, оболочка, пароль, членство в группах.
*   Команды: id <имя>, finger <имя>, cat /etc/passwd, getent passwd <имя>, groups <имя>.

3. Файловая система и примеры:
*   ФС: Способ организации данных на диске.
*   Примеры:
    *   ext4: Linux, журналируемая.
    *   XFS: Linux, высокопроизводительная, журналируемая.
    *   NTFS: Windows, журналируемая.
    *   FAT32: Совместимая, без журналирования, ограничение 4 ГБ.
    *   APFS: macOS, современная, оптимизирована для SSD.

4. Просмотр смонтированных ФС:
*   df -h, mount.

5. Удаление зависшего процесса:
*   1. ps aux | grep <имя>/top/htop (определить PID).
*   2. kill <PID>/kill -9 <PID>.

# Список литературы{.unnumbered}

::: {#refs}
:::
