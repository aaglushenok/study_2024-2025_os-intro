---
## Front matter
title: "Лабораторная работа №5. Управление системными службами"
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

Получить навыки управления системными службами операционной системы посред ством systemd.

# Выполнение лабораторной работы

## Управление сервисами 

1. Получите полномочия администратора.
2. Проверьте статус службы Very Secure FTP (сервис в настоящее время отключён, так как служба Very Secure FTP не установлена).

![Задание 1-2](image/1.png){#fig:001 width=80%}

3. Установите службу Very Secure FTP.

![Задание 3](image/2.png){#fig:002 width=80%}

4. Запустите службу Very Secure FTP.
5. Проверьте статус службы Very Secure FTP (служба в настоящее время работает, но без автозапуска).
6. Добавьте службу Very Secure FTP в автозапуск при загрузке операционной системы. Затем проверьте статус службы. Удалите службу из автозапуска и снова проверьте её статус.

![Задание 4-6](image/3.png){#fig:003 width=80%}

![Задание 6](image/4.png){#fig:004 width=80%}

7. Выведите на экран символические ссылки, ответственные за запуск различных сервисов (ссылка на vsftpd.service не существует).
8. Снова добавьте службу Very Secure FTP в автозапуск и выведите на экран символические ссылки, ответственные за запуск различных сервисов (создана символическая ссылка vsftpd.service).

![Задание 7-8](image/5.png){#fig:005 width=80%}

9. Снова проверьте статус службы Very Secure FTP (состояние изменено с disabled на enabled).

![Задание 9](image/6.png){#fig:006 width=80%}

10. Выведите на экран список зависимостей юнита.

![Задание 10](image/7.png){#fig:007 width=80%}

11. Выведите на экран список юнитов, которые зависят от данного юнита.

![Задание 11](image/8.png){#fig:008 width=80%}

## Конфликты юнитов

1. Получите полномочия администратора. Установите iptables.

![Задание 1](image/9.png){#fig:009 width=80%}

2. Проверьте статус firewalld и iptables (firewalld - enable, iptables - disable).

![Задание 2](image/10.png){#fig:010 width=80%}

3. Попробуйте запустить firewalld и iptables (при запуске одной службы вторая дезактивируется или не запускается).

![Задание 3](image/11.png){#fig:011 width=80%}

4. Введите cat /usr/lib/systemd/system/firewalld.service и опишите настройки конфликтов для этого юнита при наличии (конфликт firewalld с iptables).

![Задание 4](image/12.png){#fig:012 width=80%}

5. Введите cat /usr/lib/systemd/system/iptables.service и опишите настройки конфликтов для этого юнита.

![Задание 5](image/13.png){#fig:013 width=80%}

6. Выгрузите службу iptables (на всякий случай, чтобы убедиться, что данная служба не загружена в систему). Загрузите службу firewalld.
7. Заблокируйте запуск iptables (создана символическая ссылка на /dev/null).
8. Попробуйте запустить iptables (сообщение об ошибке, указывающее, что служба замаскирована).
9. Попробуйте добавить iptables в автозапуск (сервис неактивен, а статус загрузки замаскированный).

![Задание 6-9](image/14.png){#fig:014 width=80%}

## Изолируемые цели

1. Получите полномочия администратора. Перейдите в каталог systemd и найдите список всех целей, которые можно изолировать.
2. Переключите операционную систему в режим восстановления. При этом необходимо ввести пароль root на консоли сервера для входа в систему.

![Задание 1-2](image/15.png){#fig:015 width=80%}

3. Перезапустите операционную систему следующим образом:
systemctl isolate reboot.target

![Задание 3](image/16.png){#fig:016 width=80%}

## Цель по умолчанию 

1. Получите полномочия администратора. Выведите на экран цель, установленную по умолчанию.
2. Для запуска по умолчанию текстового режима введите systemctl set-default multi-user.target. Перегрузите систему командой reboot. Убедитесь, что система загрузилась в текстовом режиме. Для запуска по умолчанию графического режима введите systemctl set-default graphical.target. Вновь перегрузите систему командой reboot.

![Задание 1-2](image/17.png){#fig:017 width=80%}

![Задание 1-2](image/18.png){#fig:018 width=80%}

# Контрольные вопросы

1. Что такое юнит (unit)? Приведите примеры.  
Юнит — это базовый объект systemd, описывающий службу, сокет, устройство или точку монтирования. Примеры: nginx.service, tmp.mount.

2. Какая команда позволяет вам убедиться, что цель больше не входит в список автоматического запуска при загрузке системы?  
Чтобы убедиться, что цель не запускается автоматически, используйте команду: systemctl disable цель.target.

3. Какую команду вы должны использовать для отображения всех сервисных юнитов, которые в настоящее время загружены?  
Для отображения всех загруженных сервисных юнитов используйте команду: systemctl list-units --type=service.

4. Как создать потребность (wants) в сервисе?  
Чтобы создать потребность в сервисе, создайте символическую ссылку в директории .wants целевого юнита: ln -s /usr/lib/systemd/system/сервис.service /etc/systemd/system/цель.target.wants/.

5. Как переключить текущее состояние на цель восстановления (rescue target)?  
Чтобы переключиться на цель восстановления, используйте команду: systemctl rescue.

6. Поясните причину получения сообщения о том, что цель не может быть изолирована.  
Цель не может быть изолирована, если зависимости между юнитами не позволяют отключить необходимые службы или если цель не поддерживает изоляцию.

7. Вы хотите отключить службу systemd, но, прежде чем сделать это, вы хотите узнать, какие другие юниты зависят от этой службы. Какую команду вы бы использовали?  
Чтобы узнать, какие юниты зависят от службы, используйте команду: systemctl list-dependencies служба.service --reverse.

# Выводы

В ходе выполнения лабораторной работы №5 мне удалось получить навыки управления системными службами операционной системы посредством systemd.

# Список литературы{.unnumbered}

::: {#refs}
:::
