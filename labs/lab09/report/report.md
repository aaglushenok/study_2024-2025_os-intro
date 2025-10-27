---
## Front matter
title: "Лабораторная работа №9. Управление SELinux"
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

Получить навыки работы с контекстом безопасности и политиками SELinux.

# Задание  

1. Продемонстрируйте навыки по управлению режимами SELinux (см. раздел 9.4.1).
2. Продемонстрируйте навыки по восстановлению контекста безопасности SELinux (см.
раздел 9.4.2).
3. Настройте контекст безопасности для нестандартного расположения файлов веб-
службы (см. раздел 9.4.3).
4. Продемонстрируйте навыки работы с переключателями SELinux (см. раздел 9.4.4).

# Выполнение лабораторной работы

## Управление режимами SELinux

1. Запустите терминал и получите полномочия администратора: su -
2. Просмотрите текущую информацию о состоянии SELinux: sestatus -v (статус SELinux - включен/enabled, режим - принудительный/enforcing)

![Задание 1-2](image/1.png){#fig:001 width=80%}

3. Посмотрите, в каком режиме работает SELinux: getenforce (По умолчанию SELinux находится в режиме принудительного исполнения (Enforcing)).
4. Измените режим работы SELinux на разрешающий (Permissive): setenforce 0, и снова введите getenforce

![Задание 3-4](image/2.png){#fig:002 width=80%}

5. В файле /etc/sysconfig/selinux с помощью редактора установите SELINUX=disabled. Перезагрузите систему.

![Задание 5](image/3.png){#fig:003 width=80%}

6. После перезагрузки запустите терминал и получите полномочия администратора
7. Посмотрите статус SELinux: getenforce (SELinux теперь отключён).
8. Попробуйте переключить режим работы SELinux: setenforce 1 (нельзя переключаться между отключённым и принудительным режимом без перезагрузки системы)

![Задание 6-8](image/4.png){#fig:004 width=80%}

9. Откройте файл /etc/sysconfig/selinux с помощью редактора и установите: SELINUX=enforcing. Перезагрузите систему.

![Задание 9](image/5.png){#fig:005 width=80%}

10. Во время загрузки системы вы возникали предупреждающие сообщения
о необходимости восстановления меток SELinux
11. После перезагрузки в терминале с полномочиями администратора просмотрите текущую информацию о состоянии SELinux: sestatus -v (режим - принудительный/enforcing)

![Задание 10-11](image/6.png){#fig:006 width=80%}

## Использование restorecon для восстановления контекста безопасности

1. Запустите терминал и получите полномочия администратора.
2. Посмотрите контекст безопасности файла /etc/hosts: ls -Z /etc/hosts (у файла метка контекста net_conf_t)
3. Скопируйте файл /etc/hosts в домашний каталог: cp /etc/hosts ~. Проверьте контекст файла ~/hosts: ls -Z ~/hosts (копирование считается созданием нового файла -> параметр контекста в домашнем каталоге станет admin_home_t)

![Задание 1-3](image/7.png){#fig:007 width=80%}

4. Попытайтесь перезаписать существующий файл hosts из домашнего каталога в каталог /etc: mv ~/hosts /etc
5. Убедитесь, что тип контекста по-прежнему установлен на admin_home_t: ls -Z /etc/hosts

![Задание 4-5](image/8.png){#fig:008 width=80%}

6. Исправьте контекст безопасности: restorecon -v /etc/hosts. Опция -v покажет процесс изменения.
7. Убедитесь, что тип контекста изменился: ls -Z /etc/hosts
8. Для массового исправления контекста безопасности на файловой системе введите touch /.autorelabel и перезагрузите систему (во время перезапуска клавиша Esc -> видим загрузочные сообщения, файловая система перемаркирована)

![Задание 6-8](image/9.png){#fig:009 width=80%}

![Задание 8](image/10.png){#fig:010 width=80%}

## Настройка контекста безопасности для нестандартного расположения файлов веб-сервера

1. Запустите терминал и получите полномочия администратора.
2. Установите необходимое программное обеспечение: dnf -y install httpd, dnf -y install lynx

![Задание 1-2](image/11.png){#fig:011 width=80%}

3. Создайте новое хранилище для файлов web-сервера: mkdir /web
4. Создайте файл index.html в каталоге с контентом веб-сервера: cd /web, touch index.html и поместите в файл следующий текст: Welcome to my web-server

![Задание 3-4](image/12.png){#fig:012 width=80%}

![Задание 3-4](image/13.png){#fig:013 width=80%}

5. В файле /etc/httpd/conf/httpd.conf закомментируйте лишние строки и добавьте необходимые

![Задание 5](image/14.png){#fig:014 width=80%}

![Задание 5](image/15.png){#fig:015 width=80%}

6. Запустите веб-сервер и службу httpd: systemctl start httpd, systemctl enable httpd

![Задание 6](image/16.png){#fig:016 width=80%}

7. В терминале под учётной записью своего пользователя при обращении к веб-серверу в текстовом браузере lynx: lynx http://localhost (веб-страница Red Hat, а не содержимое только что созданного файла index.html)

![Задание 7](image/17.png){#fig:017 width=80%}

8. В терминале с полномочиями администратора примените новую метку контекста к /web: semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?"
9. Восстановите контекст безопасности: restorecon -R -v /web
10. В терминале под учётной записью своего пользователя снова обратитесь к веб-серверу: lynx http://localhost (после перезогрузки системы получаем доступ к своей пользовательской веб-странице)

![Задание 8-10](image/18.png){#fig:018 width=80%}

![Задание 10](image/19.png){#fig:019 width=80%}

## Работа с переключателями SELinux

1. Запустите терминал и получите полномочия администратора.
2. Посмотрите список переключателей SELinux для службы ftp: getsebool -a | grep ftp (переключатель ftpd_anon_write с текущим значением off)

![Задание 1-2](image/20.png){#fig:020 width=80%}

3. Для службы ftpd-anon посмотрите список переключателей: semanage boolean -l | grep ftpd_anon (один переключатель, позволяет анонимную запись, выключен)
4. Измените текущее значение переключателя для службы ftpd_anon_write с off на on: setsebool ftpd_anon_write on
5. Повторно посмотрите список переключателей SELinux для службы ftpd_anon_write: getsebool ftpd_anon_write
6. Посмотрите список переключателей: semanage boolean -l | grep ftpd_anon (настройка времени выполнения включена, но постоянная настройка выключена)

![Задание 3-6](image/21.png){#fig:021 width=80%}

7. Измените постоянное значение переключателя для службы ftpd_anon_write с off на on: setsebool -P ftpd_anon_write on
8. Посмотрите список переключателей: semanage boolean -l | grep ftpd_anon ((настройка времени выполнения включена, постоянная настройка включена)

![Задание 7-8](image/22.png){#fig:022 width=80%}

## Контрольные вопросы 

1. Чтобы временно поставить SELinux в разрешающем режиме, используйте команду: setenforce 0

2. Чтобы получить список всех доступных переключателей SELinux, используйте команду: getsebool -a

3. Имя пакета для получения легко читаемых сообщений SELinux: setroubleshoot

4. Чтобы применить тип контекста httpd_sys_content_t к каталогу /web, выполните команды: semanage fcontext -a -t httpd_sys_content_t '/web(/.*)?' и затем restorecon -R /web

5. Чтобы полностью отключить SELinux, нужно изменить файл: /etc/selinux/config

6. SELinux регистрирует все свои сообщения в: /var/log/audit/audit.log

7. Чтобы получить информацию о типах контекстов для службы ftp, используйте команду: sesearch -A -s ftpd_t

8. Самый простой способ проверить, связана ли проблема с SELinux: временно переключиться в разрешающий режим командой setenforce 0 и проверить, сохраняется ли проблема.

# Выводы

В ходе выполнения лабораторной работы №9 мне удалось получить навыки работы с контекстом безопасности и политиками SELinux.

# Список литературы{.unnumbered}

::: {#refs}
:::
