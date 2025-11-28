---
## Front matter
title: "Лабораторная работа №13. Фильтр пакетов"
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

Получить навыки настройки пакетного фильтра в Linux.

# Задание  

1. Используя firewall-cmd:
– определить текущую зону по умолчанию;
– определить доступные для настройки зоны;
– определить службы, включённые в текущую зону;
– добавить сервер VNC в конфигурацию брандмауэра.
2. Используя firewall-config:
– добавьте службы http и ssh в зону public;
– добавьте порт 2022 протокола UDP в зону public;
– добавьте службу ftp.
3. Выполните задание для самостоятельной работы (раздел 13.5).

# Выполнение лабораторной работы

## Управление брандмауэром с помощью firewall-cmd

1. Получите полномочия администратора: su -
2. Определите текущую зону по умолчанию: firewall-cmd --get-default-zone
3. Определите доступные зоны: firewall-cmd --get-zones

![Задание 1-3](image/1.png){#fig:001 width=80%}

4. Посмотрите службы, доступные на вашем ПК: firewall-cmd --get-services

![Задание 4](image/2.png){#fig:002 width=80%}

5. Определите доступные службы в текущей зоне: firewall-cmd --list-services

![Задание 5](image/3.png){#fig:003 width=80%}

6. Сравните результаты вывода информации при использовании команды firewall-cmd --list-all и команды firewall-cmd --list-all --zone=public

![Задание 6](image/4.png){#fig:004 width=80%} 

Пояснение: вывод идентичен, тк в первом случае он для текущей папки, те public, а во втором случае для конкретно заданной папки (та же public)

7. Добавьте сервер VNC в конфигурацию брандмауэра: firewall-cmd --add-service=vnc-server
8. Проверьте, добавился ли vnc-server в конфигурацию: firewall-cmd --list-all

![Задание 7-8](image/5.png){#fig:005 width=80%}

Пояснение: да, добавился, но как запущенный, а не как постоянный 

9. Перезапустите службу firewalld: systemctl restart firewalld
10. Проверьте, есть ли vnc-server в конфигурации: firewall-cmd --list-all

![Задание 9-10](image/6.png){#fig:006 width=80%}

Пояснение: служба vnc-server больше не указана, тк была добавленна в качестве запущенной, а не перманентной

11. Добавьте службу vnc-server ещё раз, но постоянной, используя firewall-cmd --add-service=vnc-server --permanent
12. Проверьте наличие vnc-server в конфигурации: firewall-cmd --list-all

![Задание 11-12](image/7.png){#fig:007 width=80%}

Пояснение: VNC-сервер не указан, тк службы, которые были добавлены в конфигурацию на диске, автоматически не добавляются в конфигурацию времени выполнения.

13. Перезагрузите конфигурацию firewalld и просмотрите конфигурацию времени
выполнения: firewall-cmd --reload, firewall-cmd --list-all

![Задание 13](image/8.png){#fig:008 width=80%}

Пояснение: после перезагрузки видим, что VNC-сервер отображается в списке сервисов

14. Добавьте в конфигурацию межсетевого экрана порт 2022 протокола TCP: firewall-cmd --add-port=2022/tcp --permanent. Затем перезагрузите конфигурацию firewalld: firewall-cmd --reload
15. Проверьте, что порт добавлен в конфигурацию: firewall-cmd --list-all

![Задание 14-15](image/9.png){#fig:009 width=80%}

## Управление брандмауэром с помощью firewall-config

1. Откройте терминал и под учётной записью своего пользователя запустите интерфейс GUI firewall-config: firewall-config

![Задание 1](image/10.png){#fig:010 width=80%}

2. Нажмите выпадающее меню рядом с параметром Configuration . Откройте раскрывающийся список и выберите Permanent . Это позволит сделать постоянными все изменения, которые вы вносите при конфигурировании.

![Задание 2](image/11.png){#fig:01 width=80%}

3. Выберите зону public и отметьте службы http, https и ftp, чтобы включить их.

![Задание 3](image/12.png){#fig:012 width=80%}

4. Выберите вкладку Ports и на этой вкладке нажмите Add . Введите порт 2022 и протокол udp, нажмите ОК , чтобы добавить их в список.

![Задание 4](image/13.png){#fig:013 width=80%}

5. Закройте утилиту firewall-config.
6. В окне терминала введите firewall-cmd --list-all (изменения ещё не вступили в силу, тк мы настроили их как постоянные изменения, а не как
изменения времени выполнения)

![Задание 5-6](image/14.png){#fig:014 width=80%}

7. Перегрузите конфигурацию firewall-cmd: firewall-cmd --reload и выведите список доступных сервисов: firewall-cmd --list-all (изменения применены)

![Задание 7](image/15.png){#fig:015 width=80%}

## Самостоятельная работа

1. Создайте конфигурацию межсетевого экрана, которая позволяет получить доступ к службам: telnet; imap; pop3; smtp.
2. Сделайте это как в командной строке (для службы telnet), так и в графическом интерфейсе (для служб imap, pop3, smtp).

Для telnet: добавляем через команду "...add srvice=..." :

![Задание 1-2](image/16.png){#fig:016 width=80%}

Для остальных: firewalld-config -> конфигурация: постоянная -> public -> отмечаем заданные службы галочкой

![Задание 1-2](image/17.png){#fig:017 width=80%}

3. Убедитесь, что конфигурация является постоянной и будет активирована после перезагрузки компьютера.

![Задание 3](image/18.png){#fig:018 width=80%}

## Контрольные вопросы 

1. Какая служба должна быть запущена перед началом работы с менеджером конфигурации брандмауэра firewall-config?
Должна быть запущена служба firewalld.

2. Какая команда позволяет добавить UDP-порт 2355 в конфигурацию брандмауэра в зоне по умолчанию?
Команда: firewall-cmd --add-port=2355/udp

3. Какая команда позволяет показать всю конфигурацию брандмауэра во всех зонах?
Команда: firewall-cmd --list-all-zones

4. Какая команда позволяет удалить службу vnc-server из текущей конфигурации брандмауэра?
Команда: firewall-cmd --remove-service=vnc-server

5. Какая команда firewall-cmd позволяет активировать новую конфигурацию, добавленную опцией --permanent?
Команда: firewall-cmd --reload

6. Какой параметр firewall-cmd позволяет проверить, что новая конфигурация была добавлена в текущую зону и теперь активна?
Параметр: --list-all

7. Какая команда позволяет добавить интерфейс eno1 в зону public?
Команда: firewall-cmd --zone=public --add-interface=eno1

8. Если добавить новый интерфейс в конфигурацию брандмауэра, пока не указана зона, в какую зону он будет добавлен?
Он будет добавлен в зону по умолчанию.
   
# Вывод

В ходе выполнения лабораторной работы №13 мне удалось получить навыки настройки пакетного фильтра в Linux.

# Список литературы{.unnumbered}

::: {#refs}
:::
