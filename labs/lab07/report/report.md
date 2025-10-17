---
## Front matter
title: "Лабораторная работа №7. Управление журналами событий в системе"
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

Получить навыки работы с журналами мониторинга различных событий в системе.

# Задание  

1. Продемонстрируйте навыки работы с журналом мониторинга событий в реальном
времени (см. раздел 7.4.1).
2. Продемонстрируйте навыки создания и настройки отдельного файла конфигурации
мониторинга отслеживания событий веб-службы (см. раздел 7.4.2).
3. Продемонстрируйте навыки работы с journalctl (см. раздел 7.4.3).
4. Продемонстрируйте навыки работы с journald (см. раздел 7.4.4).

# Выполнение лабораторной работы

## Мониторинг журнала системных событий в реальном времени 

1. Запустите три вкладки терминала и в каждом из них получите полномочия администратора: su -

![Задание 1](image/1.png){#fig:001 width=80%}

2. На второй вкладке терминала запустите мониторинг системных событий в реальном времени: tail -f /var/log/messages

![Задание 2](image/2.png){#fig:002 width=80%}

3. В третьей вкладке терминала вернитесь к учётной записи своего пользователя (Ctrl + d ) и попробуйте получить полномочия администратора, но введите неправильный пароль. Во второй вкладке терминала с мониторингом событий появится сообщение «FAILED SU (to root) username ...». Отображаемые на экране сообщения также фиксируются в файле /var/log/messages.

![Задание 3](image/3.png){#fig:003 width=80%}

![Задание 3](image/4.png){#fig:004 width=80%}

4. В третьей вкладке терминала из оболочки пользователя введите
logger hello. Во второй вкладке терминала с мониторингом событий вы увидите сообщение, которое также будет зафиксировано в файле /var/log/messages.
5. Во второй вкладке терминала с мониторингом остановите трассировку файла сообщений мониторинга реального времени, используя Ctrl + c. Затем запустите мониторинг сообщений безопасности (последние 20 строк соответствующего файла логов): tail -n 20 /var/log/secure. Вы увидите сообщения, которые ранее были зафиксированы во время ошибки авто-
ризации при вводе команды su.

![Задание 4-5](image/5.png){#fig:005 width=80%}

![Задание 4-5](image/6.png){#fig:006 width=80%}

![Задание 4-5](image/7.png){#fig:007 width=80%}

## Изменение правил rsyslog.conf

1. В первой вкладке терминала установите Apache, если он не был ранее инсталлирован: dnf -y install httpd

![Задание 1](image/8.png){#fig:008 width=80%}

2. После окончания процесса установки запустите веб-службу: systemctl start httpd, systemctl enable httpd

![Задание 2](image/9.png){#fig:009 width=80%}

3. Во второй вкладке терминала посмотрите журнал сообщений об ошибках веб-службы: tail -f /var/log/httpd/error_log. Чтобы закрыть трассировку файла журнала, используйте Ctrl + c .

![Задание 3](image/10.png){#fig:010 width=80%}

4. В третьей вкладке терминала получите полномочия администратора и в файле конфигурации /etc/httpd/conf/httpd.conf в конце добавьте строку: ErrorLog syslog:local1

![Задание 4](image/11.png){#fig:011 width=80%}

5. В каталоге /etc/rsyslog.d создайте файл мониторинга событий веб-службы: cd /etc/rsyslog.d, touch httpd.conf. Открыв его на редактирование, пропишите в нём local1.* -/var/log/httpd-error.log. Эта строка позволит отправлять все сообщения, получаемые для объекта local1 (который теперь используется службой httpd), в файл /var/log/httpd-error.log.

![Задание 5](image/12.png){#fig:012 width=80%}

![Задание 5](image/13.png){#fig:013 width=80%}

6. Перейдите в первую вкладку терминала и перезагрузите конфигурацию rsyslogd и веб-службу: systemctl restart rsyslog.service, systemctl restart httpd. Все сообщения об ошибках веб-службы теперь будут записаны в файл /var/log/httpd-error.log

![Задание 6](image/14.png){#fig:014 width=80%}

7. В третьей вкладке терминала создайте отдельный файл конфигурации для мониторинга отладочной информации: cd /etc/rsyslog.d, touch debug.conf. В этом же терминале введите echo "*.debug /var/log/messages-debug" > /etc/rsyslog.d/debug.conf

![Задание 7](image/15.png){#fig:015 width=80%}

8. В первой вкладке терминала снова перезапустите rsyslogd: systemctl restart rsyslog.service

![Задание 8](image/16.png){#fig:016 width=80%}

9. Во второй вкладке терминала запустите мониторинг отладочной информации: tail -f /var/log/messages-debug

![Задание 9](image/17.png){#fig:017 width=80%}

10. В третьей вкладке терминала введите: logger -p daemon.debug "Daemon Debug Message"

![Задание 10](image/18.png){#fig:018 width=80%}

11. В терминале с мониторингом посмотрите сообщение отладки. Чтобы закрыть трассировку файла журнала, используйте Ctrl + c 

![Задание 11](image/19.png){#fig:019 width=80%}

## Использование journalctl

1. Во второй вкладке терминала посмотрите содержимое журнала с событиями с момента последнего запуска системы: journalctl. Для пролистывания журнала используйте или Enter (построчный просмотр), или пробел (постраничный просмотр). Для выхода из просмотра используйте q .

![Задание 1](image/20.png){#fig:020 width=80%}

2. Просмотр содержимого журнала без использования пейджера: journalctl --no-pager

![Задание 2](image/21.png){#fig:021 width=80%}

4. Для использования фильтрации просмотра конкретных параметров журнала введите journalctl и дважды нажмите клавишу Tab .

![Задание 4](image/22.png){#fig:022 width=80%}

![Задание 4](image/23.png){#fig:0232 width=80%}

5. Просмотрите события для UID0: journalctl _UID=0

![Задание 5](image/24.png){#fig:024 width=80%}

6. Для отображения последних 20 строк журнала введите journalctl -n 20

7. Для просмотра только сообщений об ошибках введите journalctl -p err

![Задание 6-7](image/25.png){#fig:025 width=80%}

8. Если вы хотите просмотреть сообщения журнала, записанные за определённый период времени, вы можете использовать параметры --since и --until. Обе опции принимают параметр времени в формате YYYY-MM-DD hh:mm:ss. Кроме того, вы можете использовать yesterday, today и tomorrow в качестве параметров. Например, для просмотра всех сообщений со вчерашнего дня введите journalctl --since yesterday

![Задание 8](image/26.png){#fig:026 width=80%}

9. Если вы хотите показать все сообщения с ошибкой приоритета, которые были зафиксированы со вчерашнего дня, то используйте journalctl --since yesterday -p err

![Задание 9](image/27.png){#fig:027 width=80%}

10. Если вам нужна детальная информация, то используйте journalctl -o verbose

![Задание 10](image/28.png){#fig:028 width=80%}

11. Для просмотра дополнительной информации о модуле sshd введите journalctl _SYSTEMD_UNIT=sshd.service

![Задание 11](image/29.png){#fig:029 width=80%}

## Постоянный журнал journald

1. Запустите терминал и получите полномочия администратора.
2. Создайте каталог для хранения записей журнала: mkdir -p /var/log/journal
3. Скорректируйте права доступа для каталога /var/log/journal, чтобы journald смог записывать в него информацию: chown root:systemd-journal /var/log/journal, chmod 2755 /var/log/journal
4. Для принятия изменений необходимо или перезагрузить систему, или использовать команду: killall -USR1 systemd-journald
5. Журнал systemd теперь постоянный. Если вы хотите видеть сообщения журнала с момента последней перезагрузки, используйте: journalctl -b

![Задание 1-5](image/30.png){#fig:030 width=80%}

![Задание 1-5](image/31.png){#fig:031 width=80%}

## Контрольные вопросы 

1. Какой файл используется для настройки rsyslogd?  
Файл для настройки rsyslogd - /etc/rsyslog.conf.

2. В каком файле журнала rsyslogd содержатся сообщения, связанные с аутентификацией?  
Сообщения, связанные с аутентификацией, содержатся в файле /var/log/auth.log.

3. Если вы ничего не настроите, то сколько времени потребуется для ротации файлов журналов?  
Если ничего не настраивать, ротация файлов журналов происходит еженедельно.

4. Какую строку следует добавить в конфигурацию для записи всех сообщений с приоритетом info в файл /var/log/messages.info?  
Для записи всех сообщений с приоритетом info в файл /var/log/messages.info следует добавить строку: *.info /var/log/messages.info.

5. Какая команда позволяет вам видеть сообщения журнала в режиме реального времени?  
Сообщения журнала в режиме реального времени позволяет видеть команда tail -f /var/log/syslog.

6. Какая команда позволяет вам видеть все сообщения журнала, которые были написаны для PID 1 между 9:00 и 15:00?  
Сообщения журнала для PID 1 между 9:00 и 15:00 позволяет видеть команда: journalctl _PID=1 --since 09:00 --until 15:00.

7. Какая команда позволяет вам видеть сообщения journald после последней перезагрузки системы?  
Сообщения journald после последней перезагрузки системы позволяет видеть команда journalctl -b.

8. Какая процедура позволяет сделать журнал journald постоянным?  
Сделать журнал journald постоянным позволяет процедура создания директории /var/log/journal.

# Выводы

В ходе выполнения лабораторной работы №7 мне удалось получить навыки работы с журналами мониторинга различных событий в системе.

# Список литературы{.unnumbered}

::: {#refs}
:::
