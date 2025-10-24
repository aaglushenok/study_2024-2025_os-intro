---
## Front matter
lang: ru-RU
title: Лабораторная работы №8. Планировщики событий.
subtitle: Презентация
author:
  - Глушенок А. А.
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 24 октября 2025

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
---

## Докладчик

:::::::::::::: {.columns align=center}
::: {.column width="70%"}

  * Глушенок Анна Александровна
  * Студент НПИбд-01-24
  * Факультет физико-математических и естественных наук
  * Российский университет дружбы народов
  * [1132246844@pfur.ru](mailto:1132246844@pfur.ru)
  * <https://github.com/aaglushenok>

:::
::: {.column width="30%"}

:::
::::::::::::::

## Цель работы

Получение навыков работы с планировщиками событий cron и at.

## Задание  

1. Выполните задания по планированию задач с помощью crond (см. раздел 8.4.1).
2. Выполните задания по планированию задач с помощью atd (см. раздел 8.4.2).

# Выполнение лабораторной работы

# Планирование задач с помощью cron

## Планирование задач с помощью cron

1. Запустите терминал и получите полномочия администратора: su -
2. Посмотрите статус домена crond: systemctl status crond -l (статус - active (running))

![Задание 1-2](image/1.png){#fig:001 width=40%}

## Планирование задач с помощью cron

3. Посмотрите содержимое файла конфигурации /etc/crontab: cat /etc/crontab
4. Посмотрите список заданий в расписании: crontab -l. Ничего не отобразится, так как расписание ещё не задано.

![Задание 3-4](image/2.png){#fig:002 width=40%}

## Планирование задач с помощью cron

5. Откройте файл расписания на редактирование: crontab -e. Добавьте следующую строку в файл расписания: */1 * * * * logger This message is written from root cron. Закройте сеанс редактирования и сохраните изменения, используя Esc :wq

![Задание 5](image/3.png){#fig:003 width=40%}

## Планирование задач с помощью cron

6. Посмотрите список заданий в расписании: crontab -l. В расписании должна появиться запись о запланированном событии.
7. Не выключая систему, через некоторое время (2–3 минуты) просмотрите журнал системных событий: grep written /var/log/messages

![Задание 6-7](image/4.png){#fig:004 width=40%}

## Планирование задач с помощью cron

8. Измените запись в расписании crontab на следующую: 0 */1 * * 1-5 logger This message is written from root cron

![Задание 8](image/5.png){#fig:005 width=40%}

## Планирование задач с помощью cron

9. Посмотрите список заданий в расписании: crontab -l
10. Перейдите в каталог /etc/cron.hourly и создайте в нём файл сценария с именем eachhour: cd /etc/cron.hourly, touch eachhour

![Задание 9-10](image/6.png){#fig:006 width=40%}

## Планирование задач с помощью cron

11. Откройте файл eachhour для редактирования и пропишите в нём следующий скрипт: #!/bin/sh, logger This message is written at $(date)

![Задание 11](image/7.png){#fig:007 width=40%}

## Планирование задач с помощью cron

12. Сделайте файл сценария eachhour исполняемым: chmod +x eachhour
13. Теперь перейдите в каталог /etc/crond.d и создайте в нём файл с расписанием eachhour: cd /etc/cron.d, touch eachhour. Откройте этот файл для редактирования и поместите в него следующее содержимое: 11 * * * * root logger This message is written from /etc/cron.d

![Задание 12-13](image/8.png){#fig:008 width=40%}

## Планирование задач с помощью cron

![Задание 12-13](image/9.png){#fig:009 width=40%}

## Планирование задач с помощью cron

14. Не выключая систему, через некоторое время (2–3 часа) просмотрите журнал системных событий: grep written /var/log/messages. По журналу определите, был ли осуществлён запуск сценария eachhour в соответствии с заданным расписанием (Отвтет: да, был)

![Задание 14](image/10.png){#fig:010 width=40%}

# Планирование заданий с помощью at

## Планирование заданий с помощью at

1. Запустите терминал и получите полномочия администратора: su -
2. Проверьте, что служба atd загружена и включена: systemctl status atd

![Задание 1-2](image/11.png){#fig:011 width=40%}

## Планирование заданий с помощью at

3. Задайте выполнение команды logger message from at в 9:30. Для этого введите at 9:30. Затем введите logger message from at. Используйте Ctrl + d , чтобы закрыть оболочку.
4. Убедитесь, что задание действительно запланировано: atq. С помощью команды grep 'from at' /var/log/messages посмотрите, появилось
ли соответствующее сообщение в лог-файле в указанное вами время.

![Задание 3-4](image/12.png){#fig:012 width=40%}

## Выводы

В ходе выполнения лабораторной работы №8 мне удалось получить навыки работы с планировщиками событий cron и at.

# Благодарю за внимание!
