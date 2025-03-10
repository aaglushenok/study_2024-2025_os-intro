---
## Front matter
title: "Лабораторная работа № 1. Установка ОС Linux."
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

# Задание

1. Установить операционную систему.
2. Установить обновления, отключить SELinux.
3. Настроить раскладку клавиатуры.
4. Установить имя пользователя и название хоста.
5. Установить ПО ждя создания документации.

# Выполнение лабораторной работы

Зададим имя виртуальной машины, выберем папку хранения и Образ диска ISO:

![Создание ВМ](image/1.PNG){#fig:001 width=80%}

Выделим основную память, процессоры:

![Оборудование](image/2.PNG){#fig:002 width=80%}

Зададим конфигурацию жесткого диска, размер диска:

![Виртуальный жесткий диск](image/3.PNG){#fig:003 width=80%}

Выделим видеопамять, включим 3D-ускорение:

![Настройка дисплея](image/4.PNG){#fig:004 width=80%}

Выполним запуск виртуальной машины. Пропишем команду liveinst, выберем место установки, создадим аккаунт пользователя и учетную запись root: 

![Ввод команды liveinst](image/5.PNG){#fig:005 width=80%}

![Обзор установки](image/6.PNG){#fig:006 width=80%}

![Создание пользователя](image/7.PNG){#fig:007 width=80%}

![Аккаунт администратора](image/8.PNG){#fig:008 width=80%}

Осуществим вход в ОС, переключимся на роль супер-пользователя, установим средства разработки, обновим пакеты:

![Вход в ОС, установка обновлений](image/9.PNG){#fig:009 width=80%}

Повысим комфорт работы в консоли; Установим автоматическое обновление, поставим таймер:

![Повышение комфорта работы](image/10.PNG){#fig:010 width=80%}

В файле /etc/selinux/config заменим значение SELINUX=enforcing н азначение SELINUX=permissive. Перезагрузим виртуальную машину:

![Внесение изменений в файл](image/11.PNG){#fig:011 width=80%}

Запустим терминальный мультиплексор tmux. Создадим конфигурационный файл ~/config/sway/config.d/96-systemkeyboard-config.conf:

![Создание конфигурационного файла](image/12.PNG){#fig:012 width=80%}

Отредактируем конфигурационный файл ~/config/sway/config.d/96-systemkeyboard-config.conf:

![Редактирование 1-го конфигурационного файла](image/13.PNG){#fig:013 width=80%}

Запустим и отредактируем конфигурационный файл /etc/X11/xorg.conf.d/00-keyboard.conf:

![Запуск конфигурационных файлов](image/14.PNG){#fig:014 width=80%}

![Редактирование 2-го конфигурационного файла](image/15.PNG){#fig:015 width=80%}

Запустим терминальный мультиплексор tmux, переключимся на роль супер-пользователя. Создадим пользователя и его пароль. Установим имя хоста. Проверим, что имя хоста установлено верно: 

![Установка имени пользователя и названия хоста](image/16.PNG){#fig:016 width=80%}

Установим средство работы pandoc для работы с языком разметки MarkDown. Для работы с перекрестными ссылками скачаем пакет pandoc-crossref, версии 3.1.11.1:

![Установка ПО для создания документации](image/17.PNG){#fig:017 width=80%}

Распакуем архивы, переместим их в каталог /usr/local/bin:

![Распаковка архива](image/18.PNG){#fig:018 width=80%}

Установим дистрибутив TeXlive:

![Установка TeXlive](image/19.PNG){#fig:019 width=80%}

# Выполнение домашней работы

1. Версия ядра Linux: 6.12.15-200.
2. Частота процессора: 2496.010.
3. Модель процессора: Intel (R) Core (TM).
4. Объем доступной оперативной памяти: 5119544K.
5. Тип обнаруженного гипервизора: KVM.
6. Тип файловой системы корневого раздела: sda4.
7. Последовательность монтирования файловых систем: BTRFS, EXT4-fs.

![Выполнение домашней работы](image/20.PNG){#fig:020 width=80%}

# Ответы на контрольные вопросы 

1. Какую информацию содержит учётная запись пользователя?

Системное имя, идентификатор пользователя, идентификатор группы, полное имя, домашний каталог, начальная оболочка.

2. Укажите команды терминала и приведите примеры:

– для получения справки по команде; man <команда> (man ls)  
– для перемещения по файловой системе; cd <каталог> (cd / - перемещение в корневой каталог)  
– для просмотра содержимого каталога; ls <каталог если нужно> (ls / - содержимое корневого каталога)  
– для определения объёма каталога; du -s <каталог> (du -s /etc)  
– для создания / удаления каталогов / файлов; rm <ключ> <название файла/каталога>
Пустые каталоги можно удалять командой rmdir (если добавить ключ -s, то можно удалять и не только пустые). Также любые файлы можно удалять рекурсивно: rm -r <название файла/каталога>  
– для задания определённых прав на файл / каталог; chmod <xxx> <имя> (chmod 777 filename.txt)  
– для просмотра истории команд. history3  

3. Что такое файловая система? Приведите примеры с краткой характеристикой.

Порядок, определяющий способ организации, хранения и именования данных на носителях информации. Например ext2. Характеристика: ext2 журналируема (при сбоях можно восстановить данные). Максимальный размер файла 16гб-2гб. Максимальный размер тома 2гб-32гб. Существует единственный корневой каталог откуда исходят остальные каталоги. Максимальная длина имени файла 266 байт.

4. Как посмотреть, какие файловые системы подмонтированы в ОС?

Команда mount.

5. Как удалить зависший процесс?

Kill <PID>. Pid можно получить командой ps axu | grep “то, что мы ищем”. (kill 5099).

# Выводы

В ходе выполнения лабораторной работы №1 мне удалось приобрести практические навыки установки операционной системы на виртуальную машину, настройки минимально необходимых для дальнейшей работы сервисов.

# Список литературы{.unnumbered}

::: {#refs}
:::
