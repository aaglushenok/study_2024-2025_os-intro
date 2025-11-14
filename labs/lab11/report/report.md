---
## Front matter
title: "Лабораторная работа №11. Управление загрузкой системы"
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

Получить навыки работы с загрузчиком системы GRUB2.

# Задание  

1. Продемонстрируйте навыки по изменению параметров GRUB и записи изменений в файл конфигурации (см. раздел 11.4.1).
2. Продемонстрируйте навыки устранения неполадок при работе с GRUB (см. раздел 11.4.2).
3. Продемонстрируйте навыки работы с GRUB без использования root (см. раздел 11.4.3)

# Выполнение лабораторной работы

## Модификация параметров GRUB2

1. Запустите терминал и получите полномочия администратора: su -
2. В файле /etc/default/grub установите параметр отображения меню загрузки в течение 10 секунд: GRUB_TIMEOUT=10. Сохраните изменения в файле и закройте редактор.

![Задание 1-2](image/1.png){#fig:001 width=80%}

![Задание 1-2](image/2.png){#fig:002 width=80%}

3. Запишите изменения в GRUB2, введя в командной строке grub2-mkconfig > /boot/grub2/grub.cfg
4. Перезагрузите систему и убедитесь, что при загрузке вы видите прокрутку загрузочных сообщений

В результате видим, что автоматический запуск увеличен с 5 секунд до 10.

![Задание 3-4](image/3.png){#fig:003 width=80%}

![Задание 3-4](image/4.png){#fig:004 width=80%}

## Устранения неполадок

1. Перегрузите систему. Появится меню GRUB, выберите строку с версией ядра и нажмите e для редактирования.
2. Прокрутите до строки, начинающейся с linux ($root)/.. (загружает ядро системы). В конце строки введите systemd.unit=rescue.target и удалите опции rhgb и quit
3. Нажмите Ctrl + x для продолжения процесса загрузки

![Задание 1-3](image/5.png){#fig:005 width=80%}

4. Введите пароль пользователя root при появлении запроса.
5. Посмотрите список всех файлов модулей, которые загружены в настоящее время: systemctl list-units (загружена базовая системная среда, 73 юнита)

![Задание 4-5](image/6.png){#fig:006 width=80%}

6. Посмотрите задействованные переменные среды оболочки: systemctl show-environment
7. Перегрузите систему, используя команду systemctl reboot

![Задание 6-7](image/7.png){#fig:007 width=80%}

8. Как только отобразится меню GRUB, нажмите e на строке с версией ядра, чтобы войти в режим редактора. В конце строки введите systemd.unit=emergency.target и удалите опции rhgb и quit
9. Нажмите Ctrl + x для продолжения процесса загрузки.

![Задание 8-9](image/8.png){#fig:008 width=80%}

10. Введите пароль пользователя root при появлении запроса.
11. После успешного входа в систему посмотрите список всех загруженных файлов модулей: systemctl list-units (количество загружаемых файлов модулей уменьшилось до минимума, 73 юнита -> 53)
12. Перегрузите систему, используя команду: systemctl reboot

![Задание 10-12](image/9.png){#fig:009 width=80%}

## Сброс пароля root

1. Перегрузите компьютер. Когда отобразится меню GRUB, выберите строку с  версией ядра системы и нажмите e , чтобы войти в режим редактора. В конце строки введите rd.break и удалите опции rhgb и quit
2. Нажмите Ctrl + x для продолжения процесса загрузки.

![Задание 1-2](image/10.png){#fig:010 width=80%}

3. Этап загрузки системы остановится в момент загрузки initramfs, перед монтированием корневой файловой системы в каталоге /.
4. Чтобы получить доступ к системному образу для чтения и записи, наберите mount -o remount,rw /sysroot
5. Сделайте содержимое каталога /sysimage новым корневым каталогом, набрав chroot /sysroot
6. Введите команду задания пароля: passwd и установить новый пароль для пользователя root.

![Задание 3-6](image/11.png){#fig:011 width=80%}

7. На этом этапе SELinux ещё не активирован, тип контекста SELinux для файла /etc/shadow будет испорчен. Чтобы бедиться, что тип контекста установлен правильно, загрузите политику SELinux с помощью команды load_policy -i
8. Теперь вручную установите правильный тип контекста для /etc/shadow: chcon -t shadow_t /etc/shadow
9. Перезагрузите систему с помощью reboot -f и войдите в систему с изменённым паролем для root. 

![Задание 7-9](image/12.png){#fig:012 width=80%}

![Задание 7-9](image/13.png){#fig:013 width=80%}

## Контрольные вопросы 

1. Какой файл конфигурации следует изменить для применения общих изменений в GRUB2?
Файл /etc/default/grub.

2. Как называется конфигурационный файл GRUB2, в котором вы применяете изменения для GRUB2?
Конфигурационный файл /etc/default/grub.

3. После внесения изменений в конфигурацию GRUB2, какую команду вы должны выполнить, чтобы изменения сохранились и воспринялись при загрузке системы?
Команду update-grub.
   
# Вывод

В ходе выполнения лабораторной работы №11 мне удалось получить навыки работы с загрузчиком системы GRUB2.

# Список литературы{.unnumbered}

::: {#refs}
:::
