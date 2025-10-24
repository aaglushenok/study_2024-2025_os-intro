---
## Front matter
title: "Лабораторная работа №8. Планировщики событий"
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

Получение навыков работы с планировщиками событий cron и at.

# Задание  

1. Выполните задания по планированию задач с помощью crond (см. раздел 8.4.1).
2. Выполните задания по планированию задач с помощью atd (см. раздел 8.4.2).

# Выполнение лабораторной работы

## Планирование задач с помощью cron

1. Запустите терминал и получите полномочия администратора: su -
2. Посмотрите статус домена crond: systemctl status crond -l (статус - active (running))

![Задание 1-2](image/1.png){#fig:001 width=80%}

3. Посмотрите содержимое файла конфигурации /etc/crontab: cat /etc/crontab
4. Посмотрите список заданий в расписании: crontab -l. Ничего не отобразится, так как расписание ещё не задано.

![Задание 3-4](image/2.png){#fig:002 width=80%}

5. Откройте файл расписания на редактирование: crontab -e. Добавьте следующую строку в файл расписания: */1 * * * * logger This message is written from root cron. Закройте сеанс редактирования и сохраните изменения, используя Esc :wq

![Задание 5](image/3.png){#fig:003 width=80%}

Синтаксис записи */1 * * * * logger This message is written from root cron:
а) */1 * * * * - расписание выполнения:
- "*/1" - минуты: каждую 1 минуту
- "*" - часы: каждый час
- "*" - дни месяца: каждый день
- "*" - месяцы: каждый месяц
- "*" - дни недели: каждый день
б) logger This message is written from root cron - команда для выполнения:
- "logger" - утилита для записи в системный журнал
Результат: Текст будет записан в syslog с сообщением "This message is written from root cron", задание будет выполняться каждую минуту и записывать указанное сообщение в системный журнал.

6. Посмотрите список заданий в расписании: crontab -l. В расписании должна появиться запись о запланированном событии.
7. Не выключая систему, через некоторое время (2–3 минуты) просмотрите журнал системных событий: grep written /var/log/messages

![Задание 6-7](image/4.png){#fig:004 width=80%}

8. Измените запись в расписании crontab на следующую: 0 */1 * * 1-5 logger This message is written from root cron

![Задание 8](image/5.png){#fig:005 width=80%}

Синтаксис записи 0 */1 * * 1-5 logger This message is written from root cron:
а) 0 */1 * * 1-5 - расписание выполнения:
- "0" - минуты: в 0 минут каждого часа
- "*/1" - часы: каждый час (эквивалентно *)
- "*" - дни месяца: каждый день
- "*" - месяцы: каждый месяц
- "1-5" - дни недели: с понедельника по пятницу (1=понедельник, 5=пятница)
б) logger This message is written from root cron - команда для выполнения:
- "logger" - утилита для записи в системный журнал
Результат: Текст будет записан в syslog с сообщением "This message is written from root cron", задание будет выполняться в 00 минут каждого часа с понедельника по пятницу и записывать указанное сообщение в системный журнал.

9. Посмотрите список заданий в расписании: crontab -l
10. Перейдите в каталог /etc/cron.hourly и создайте в нём файл сценария с именем eachhour: cd /etc/cron.hourly, touch eachhour

![Задание 9-10](image/6.png){#fig:006 width=80%}

11. Откройте файл eachhour для редактирования и пропишите в нём следующий скрипт: #!/bin/sh, logger This message is written at $(date)

![Задание 11](image/7.png){#fig:007 width=80%}

12. Сделайте файл сценария eachhour исполняемым: chmod +x eachhour
13. Теперь перейдите в каталог /etc/crond.d и создайте в нём файл с расписанием eachhour: cd /etc/cron.d, touch eachhour. Откройте этот файл для редактирования и поместите в него следующее содержимое: 11 * * * * root logger This message is written from /etc/cron.d

![Задание 12-13](image/8.png){#fig:008 width=80%}

![Задание 12-13](image/9.png){#fig:009 width=80%}

Синтаксис записи 11 * * * * root logger This message is written from /etc/cron.d:
а) 11 * * * * - расписание выполнения:
- 11 - минуты: в 11 минут каждого часа
- * - часы: каждый час
- * - дни месяца: каждый день
- * - месяцы: каждый месяц
- * - дни недели: каждый день
- root - пользователь, от которого выполняется команда
б) logger This message is written from /etc/cron.d - команда для выполнения:
- logger - утилита для записи в системный журнал
Результат: Текст будет записан в syslog с сообщением "This message is written from /etc/cron.d", задание будет выполняться каждый час в 11 минут (01:11, 02:11, 03:11 и т.д.) от имени пользователя root и записывать указанное сообщение в системный журнал.

14. Не выключая систему, через некоторое время (2–3 часа) просмотрите журнал системных событий: grep written /var/log/messages. По журналу определите, был ли осуществлён запуск сценария eachhour в соответствии с заданным расписанием (Отвтет: да, был)

![Задание 14](image/10.png){#fig:010 width=80%}

## Планирование заданий с помощью at

1. Запустите терминал и получите полномочия администратора: su -
2. Проверьте, что служба atd загружена и включена: systemctl status atd

![Задание 1-2](image/11.png){#fig:011 width=80%}

3. Задайте выполнение команды logger message from at в 9:30. Для этого введите at 9:30. Затем введите logger message from at. Используйте Ctrl + d , чтобы закрыть оболочку.
4. Убедитесь, что задание действительно запланировано: atq. С помощью команды grep 'from at' /var/log/messages посмотрите, появилось
ли соответствующее сообщение в лог-файле в указанное вами время.

![Задание 3-4](image/12.png){#fig:012 width=80%}

## Контрольные вопросы 

1. Как настроить задание cron, чтобы оно выполнялось раз в 2 недели?
0 0 */14 * *

2. Как настроить задание cron, чтобы оно выполнялось 1-го и 15-го числа каждого месяца в 2 часа ночи?
0 2 1,15 * *

3. Как настроить задание cron, чтобы оно выполнялось каждые 2 минуты каждый день?
*/2 * * * *

4. Как настроить задание cron, чтобы оно выполнялось 19 сентября ежегодно?
0 0 19 9 *

5. Как настроить задание cron, чтобы оно выполнялось каждый четверг сентября ежегодно?
0 0 * 9 4

6. Какая команда позволяет вам назначить задание cron для пользователя alice?
crontab -u alice -e

7. Как указать, что пользователю bob никогда не разрешено назначать задания через cron?
echo "bob" >> /etc/cron.deny

8. Вам нужно убедиться, что задание выполняется каждый день, даже если сервер во время выполнения временно недоступен. Как это сделать?
Использовать anacron или настроить повторение задания при загрузке системы.

9. Какая команда позволяет узнать, запланированы ли какие-либо задания на выполнение планировщиком atd?
atq

# Выводы

В ходе выполнения лабораторной работы №8 мне удалось получить навыки работы с планировщиками событий cron и at.

# Список литературы{.unnumbered}

::: {#refs}
:::
